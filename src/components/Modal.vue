<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo">
        <img :src="photo" />
      </div>
      <div class="description">
        <h2 class="title">{{ title }}</h2>
        <p class="description">
          {{ description }}
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
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description.substring(0, 500);
  },
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

    @media (min-width: 1024px) {
      max-height: 70%;
      width: 60%;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      margin: auto;
      box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
    }
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

    @media (min-width: 1024px) {
      flex-direction: row;

      .photo {
        min-width: 50%;
        margin-right: 50px;
      }
    }

    .photo {
      max-width: auto;
      max-height: auto;
      background: black;

      img {
        width: 100%;
      }
    }

    .description {
      color: #333;
      text-align: center;
    }

    .title {
      color: darkcyan;
      text-align: center;
      margin-bottom: 20px;
    }
  }

</style>
