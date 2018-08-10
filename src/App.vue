<template>
    <div :class="[{flexStart: step === 1}, 'wrapper']">
      <transition name="slide">
      <img src="./assets/pobrane.svg" class="logo" alt="" v-if="step === 1"/>
      </transition>
      <transition name="fade">
        <HeroImage v-if="step === 0 " />
      </transition>
      <Claim v-if="step === 0 " />
      <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
      <div class="results" v-if="results && !loading && step === 1">
        <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
      </div>
      <Modal v-if="modalOpen" @closeModal="modalOpen = false" />
    </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";

import HeroImage from "@/components/HeroImage.vue";
import SearchInput from "@/components/SearchInput.vue";
import Claim from "@/components/Claim.vue";
import Item from "@/components/Item.vue";
import Modal from "@/components/Modal.vue";

const API = "https://images-api.nasa.gov/search";

export default {
  name: "App",
  components: {
    HeroImage,
    Claim,
    SearchInput,
    Item,
    Modal
  },

  data() {
    return {
      modalOpen: false,
      loading: false,
      step: 0,
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleModalOpen() {
      this.modalOpen = true;
    },
    // eslint-disable-next-line
    handleInput: debounce(function() {
      this.loading = true;
      console.log(this.searchValue);
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(response => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch(error => {
          console.log(error);
        });
    }, 500)
  }
};
</script>


<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800");
* {
  box-sizing: border-box;
}
body {
  font-family: Montserrat, sans-serif;
  margin: 0;
  padding: 0;
}
.fade-enter-active, .fade-leave-active{
  transition: opacity .3s ease;
} 
.fade-enter, .fade-leave-to{
  opacity: 0;
}
.slide-enter-active, .slide-leave-active{
  transition: margin-top .3s ease;
} 
.slide-enter, .slide-leave-to{
  margin-top: -50px;
}
.wrapper {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  min-height: 100vh;
  &.flexStart {
    justify-content: flex-start;
  }
}

.logo{
  position: absolute;
  top: 30px;
}
.results{
  margin-top:50px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px;
}
</style>
