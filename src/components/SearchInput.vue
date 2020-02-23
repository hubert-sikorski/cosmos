<template>
  <input
    id="search"
    name="search"
    placeholder="Search"
    :class="{ dark }"
    :value="value"
    @input="handleChange"
  />
</template>
<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(event) {
      this.$emit('input', event.target.value);
    },
  },
};
</script>
<style lang="scss" scoped>
input {
  margin-top: 50px;
  display: flex;
  width: 300px;
  height: 30px;
  border: none;
  border-bottom: 1px solid white;
  text-align: center;
  font-size: 20px;
  font-weight: 300;
  background: none;
  color: white;
  transition: box-shadow 1s;

  &::placeholder {
    color: white;
  }

  &:focus {
    outline: none;
    box-shadow: 0 12px 20px -12px rgba(255, 255, 255, 0.5);
  }

  @media (min-width: 1024px) {
    font-weight: 400;
  }
}

.dark {
  color: darkcyan;
  border-bottom-color: darkcyan;

  &:focus {
    box-shadow: 0 12px 20px -12px rgba(darkcyan, 0.5);
  }
}

</style>
