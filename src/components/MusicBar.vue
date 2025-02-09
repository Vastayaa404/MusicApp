<template>
  <div class="equalizer">
    <div
      v-for="(amp, index) in bars"
      :key="index"
      class="bar"
      :style="{ height: 2 * Math.max(amp, 1) + 'px' }"
    ></div>
  </div>
</template>

<script setup>
  import { ref, onBeforeUnmount, watch } from 'vue'
  import { Howl, Howler } from 'howler'

  // Принимаем проп isPlaying как Boolean
  const props = defineProps({
    isPlaying: {
      type: Boolean,
      required: true
    }
  })

  // Будем отображать 6 полос
  const numBars = 6
  const bars = ref(new Array(numBars).fill(0)) // минимальная высота 2px

  let sound = null
  let analyser = null
  let dataArray = null
  let animationFrameId = null

  // Инициализация Howler и анализатора
  const setupHowler = () => {
    if (!sound) {
      sound = new Howl({
        src: ['BringMeToLife.mp3'], // убедитесь, что файл доступен (например, положите его в папку public)
        html5: false, // используем Web Audio API
        volume: 1.0,
        onload: () => console.log('Audio loaded'),
        onloaderror: (id, error) => console.error('Audio load error:', error)
      })
    }
    if (!analyser) {
      analyser = Howler.ctx.createAnalyser()
      analyser.fftSize = 256
      const bufferLength = analyser.frequencyBinCount
      dataArray = new Uint8Array(bufferLength)
      // Инициализируем массив bars значениями по умолчанию (2px)
      bars.value = new Array(numBars).fill(0)
      
      // Перенаправляем аудиосигнал через анализатор:
      Howler.masterGain.disconnect()
      Howler.masterGain.connect(analyser)
      analyser.connect(Howler.ctx.destination)
    }
  }

  // Функция, группирующая частотные данные в 6 диапазонов
  const animate = () => {
    analyser.getByteFrequencyData(dataArray)
    const groupSize = Math.floor(dataArray.length / numBars)
    const grouped = []
    for (let i = 0; i < numBars; i++) {
      let sum = 0
      for (let j = 0; j < groupSize; j++) {
        sum += dataArray[i * groupSize + j]
      }
      const avg = sum / groupSize
      grouped.push(avg)
    }
    bars.value = grouped
    animationFrameId = requestAnimationFrame(animate)
  }

  // Отслеживаем изменение isPlaying (из родительского компонента)
  watch(() => props.isPlaying, async (newVal) => {
    if (newVal) {
      setupHowler()
      if (Howler.ctx.state === 'suspended') {
        await Howler.ctx.resume()
        console.log('AudioContext resumed')
      }
      sound.play()
      animate()
    } else {
      sound.pause()
      cancelAnimationFrame(animationFrameId)
      console.log('Audio paused')
    }
  })

  onBeforeUnmount(() => {
    cancelAnimationFrame(animationFrameId)
    if (sound) sound.stop()
  })
</script>

<style scoped>
.equalizer {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 3%;
  width: 80%;
  height: 70%;
  top: 10%;
}

.bar {
  width: 8%;
  border-radius: 2vw;
  background-color: rgb(173, 0, 0);
  transition: height 0.1s linear;
}
</style>