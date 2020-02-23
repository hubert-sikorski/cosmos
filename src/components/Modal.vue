<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo">
        <img src="../assets/logo.png" />
      </div>
      <div class="description">
        <h2 class="title">Lorem, ipsum.</h2>
        <p class="description">
          Lorem ipsum, dolor sit amet consectetur adipisicing elit. Explicabo
          facilis libero accusantium dolorem ipsum veniam, tempora est
          reprehenderit, cumque doloribus eos, sequi harum facere quos
          repellendus. Unde ducimus harum ipsam.
        </p>
      </div>
    </div>
    <div class="close" @click="$emit('closeModal')">
      &times;
    </div>
  </div>
</template>
<script>
export default {
  name: 'Modal',
};
</script>
<style lang="scss" scoped>
  .outerWrapper {
    background: #f6f6f6;
    max-width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
  }

  .close {
    position: absolute;
    right: 2rem;
    top: 1rem;
    text-decoration: none;
    font-size: 3rem;
    cursor: pointer;

    &:hover {
      color: indianred;
    }
  }

  .innerWrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    padding: 50px;

    .photo {
      width: 100%;
      height: auto;
      background: black;

      img {
        width: 100%;
      }
    }

    .description {
      color: #333;
    }
  }

</style>
