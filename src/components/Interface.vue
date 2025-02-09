<template>
  <div class="interface">
    <div class="svg-container">
      <!-- Кнопка "предыдущий трек" -->
      <svg fill="#000000" width="3vw" height="3vw" viewBox="0 0 24 24" id="previous" data-name="Flat Color" xmlns="http://www.w3.org/2000/svg" class="svg-btn">
        <path id="primary" d="M17.45,2.11a1,1,0,0,0-1.05.09l-12,9a1,1,0,0,0,0,1.6l12,9a1,1,0,0,0,1.05.09A1,1,0,0,0,18,21V3A1,1,0,0,0,17.45,2.11Z"></path>
      </svg>
      <!-- Кнопка "воспроизвести/пауза" -->
      <svg
        width="3vw"
        height="3vw"
        viewBox="-1 0 8 8"
        version="1.1"
        class="svg-btn"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        @click="onTogglePlayback"
      >
        <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
          <g id="Dribbble-Light-Preview" transform="translate(-227.000000, -3765.000000)" fill="#000000">
            <g id="icons" transform="translate(56.000000, 160.000000)">
              <path d="M172,3605 C171.448,3605 171,3605.448 171,3606 L171,3612 C171,3612.552 171.448,3613 172,3613 C172.552,3613 173,3612.552 173,3612 L173,3606 C173,3605.448 172.552,3605 172,3605 M177,3606 L177,3612 C177,3612.552 176.552,3613 176,3613 C175.448,3613 175,3612.552 175,3612 L175,3606 C175,3605.448 175.448,3605 176,3605 C176.552,3605 177,3605.448 177,3606"></path>
            </g>
          </g>
        </g>
      </svg>
      <!-- Кнопка "следующий трек" -->
      <svg fill="#000000" width="3vw" height="3vw" viewBox="0 0 24 24" id="next" data-name="Flat Color" xmlns="http://www.w3.org/2000/svg" class="svg-btn">
        <path id="primary" d="M18.6,11.2l-12-9A1,1,0,0,0,5,3V21a1,1,0,0,0,.55.89,1,1,0,0,0,1-.09l12-9a1,1,0,0,0,0-1.6Z"></path>
      </svg>
    </div>
  </div>
</template>

<script setup>
  const emit = defineEmits(['togglePlayback'])
  const onTogglePlayback = () => emit('togglePlayback')
</script>

<style scoped>
.interface {
  position: absolute;
  width: 90%;
  height: 80%;
  top: 10%;
  left: 5%;

  display: flex;
  justify-content: center;
  align-items: center;

  border-radius: 3vw;
  background: rgba(255, 255, 255, 0.27);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.15);
  backdrop-filter: blur(0.35vmin);
  transform: translateZ(0);
}

.svg-container {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 20%;
  height: 30%;
  margin-top: auto;
}

.svg-btn {
  cursor: pointer;
}
</style>