/* eslint-disable */
<template>
  <div :style="style" class="item" />
</template>
<script>
export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title,
    };
  },
  computed: {
    style() {
      return `background-image: url("${this.photo}")`;
    },
  },
};
</script>
<style lang="scss" scoped>
.item {
  width: 6.6rem;
  height: 6.6rem;
  background-size: cover;
  background-repeat: no-repeat;
  cursor: pointer;

  @media (min-width: 360px) {
    width: 7.4rem;
    height: 7.4rem;
  }

  @media (min-width: 768px) {
    width: 10rem;
    height: 10rem;
  }

  @media (min-width: 1024px) {
    width: 20rem;
    height: 20rem;
  }
}
</style>
