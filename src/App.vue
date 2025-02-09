<script setup>
  import Interface from './components/Interface.vue';
  import Musicbar from './components/MusicBar.vue';

  import { ref } from 'vue'

  const isPlaying = ref(false)
  const togglePlayback = () => isPlaying.value = !isPlaying.value
</script>

<template>
  <div class="wrapper" style="display: flex; justify-content: center; align-items: center">
    <span class="ico">&#x2764;</span>
    <Musicbar :is-playing="isPlaying" />
    <Interface @togglePlayback="togglePlayback" />
  </div>
</template>

<style>
body {
  margin: 0;
  overflow-x: hidden;
  user-select: none;
}

*,
*:before,
*:after {
  box-sizing: border-box;
}

.wrapper {
  width: 100vw;
  height: 100vh;

  background-color: rgb(240, 240, 240);
}

.ico {
  position: absolute;
  font-size: 2vh;
  top: .5%;
  left: .5%;
}
</style>
