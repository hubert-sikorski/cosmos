/* eslint-disable */
<template>
  <div class="claimWrapper">
    <h1 class="claim">COSMOS</h1>
    <p class="subclaim">
      Explore the most out of this planet pictures straight from the NASA
    </p>
    <p class="subclaim">
      The outer space in your hands
    </p>
  </div>
</template>
<script>
export default {
  name: 'Claim',
};
</script>
<style lang="scss" scoped>
.claimWrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  background: none;
  color: white;
}

.claim {
  font-size: 50px;
  margin: 0;

  @media (min-width: 768px) {
    font-size: 80px;
  }

  @media (min-width: 1024px) {
    font-size: 100px;
  }
}

.subclaim {
  margin-top: 20px;
  font-size: 13px;
  font-weight: 400;

  @media (min-width: 768px) {
    font-size: 17px;
    width: 500px;
    line-height: 1;
    letter-spacing: 1px;
  }
}
</style>
