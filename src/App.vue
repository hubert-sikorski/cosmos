<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img
        src="./assets/logo.png"
        class="logo"
        v-if="step === 1"
        @click="goToMainPage"
      />
    </transition>
    <transition name="fade">
      <Background v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput
      v-model="searchValue"
      @input="handleInput"
      :dark="step === 1"
    />
    <div class="results" v-if="results && !loading && step === 1">
      <Item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <div class="loader" v-if="step === 1 && loading" />
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import debounce from 'lodash.debounce';
import Background from '@/components/Background.vue';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Background,
    Claim,
    SearchInput,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
      console.log(item);
    },
    goToMainPage() {
      this.step = 0;
    },
    // eslint-disable-next-line
    handleInput: debounce(function() {
      this.loading = true;
      console.log(this.searchValue);
      if (this.searchValue) {
        axios
          .get(`${API}?q=${this.searchValue}&media_type=image`)
          .then((response) => {
            this.results = response.data.collection.items;
            this.loading = false;
            this.step = 1;
          })
          .catch((error) => {
            console.log(error);
          });
      }
    }, 1000),
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font-family: 'Montserrat', sans-serif;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: margin-top 0.3s ease;
}

.slide-enter,
.slide-leave-to {
  margin-top: -50px;
}

.wrapper {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  width: 100%;
  padding: 30px;
  background: none;

  &.flexStart {
    justify-content: flex-start;
  }
}

.loader {
  margin-top: 100px;
  display: inline-block;
  width: 80px;
  height: 80px;

  @media (min-width: 768px) {
    width: 90px;
    height: 90px;
  }
}

.loader:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid darkcyan;
  border-color: darkcyan transparent darkcyan transparent;
  animation: loading 1.2s linear infinite;
}

@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.logo {
  position: absolute;
  top: 15px;
  height: 2rem;
  width: 9rem;
  cursor: pointer;
}

.results {
  margin-top: 50px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px;

  @media (max-width: 767px) {
    grid-gap: 1px;
  }
}
</style>
