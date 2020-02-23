<template>
  <div class="backgroundWrapper" />
</template>
<script>
export default {
  name: 'Background',
};
</script>
<style lang="scss" scoped>
.backgroundWrapper {
  position: fixed;
  top: 0;
  z-index: -1;
  width: 100%;
  height: 100vh;
  background-image: url('../assets/background.jpg');
  background-size: cover;

  &::after {
    content: '';
    background: rgba(0, 0, 0, 0.2);
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
    width: 100%;
    height: 100vh;
  }
}
</style>
