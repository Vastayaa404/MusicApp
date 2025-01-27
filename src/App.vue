<script setup>

</script>

<template>
  <div class="wrapper" style="display: flex; justify-content: center; align-items: center">
    <span class="ico">&#x2764;</span>
    <h1 style="font-size: 5vmax;">Centered text Centered text Centered text Centered text</h1>
    <div class="interface">routes</div>
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

  background-color: red;
}

.ico {
  position: absolute;
  font-size: 2vh;
  top: .5%;
  left: .5%;
}

.interface {
  position: absolute;
  width: 90%;
  height: 80%;
  top: 10%;
  left: 5%;

  border-radius: 3vw;
  background: rgba(255, 255, 255, 0.14);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(0.8vmin);
  border: 1px solid rgb(0, 0, 0);
}
</style>
