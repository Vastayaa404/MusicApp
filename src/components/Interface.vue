<template>
  <div class="interface">
    
  </div>
</template>

<script setup>
  import { defineAsyncComponent } from 'vue';

  // Lazy loading ICOs
  const PauseIco = defineAsyncComponent(() => import('../assets/pause-svgrepo-com.svg'));
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
  background: rgba(255, 255, 255, 0.14);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(0.8vmin);
  /* border: 1px solid rgb(0, 0, 0); */
}
</style>