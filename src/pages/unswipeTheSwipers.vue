<template>
  <div class="container">
    <header-component :hotkeys="lettersArray" />
    <div class="sliderContainer">
      <slider-component v-for="(el, id) in lettersArray" :key="id" :elName="el" />
    </div>
  </div>
</template>

<script>
import HeaderComponent from '../components/HeaderComponent.vue';
import SliderComponent from '../components/SliderComponent.vue';
export default {
  components: {
    HeaderComponent,
    SliderComponent,
  },
  setup() {
    // array of names for swipers duplication
    const lettersArray = ['A', 'B', 'C', 'D', 'E', 'F'];
    return {
      lettersArray,
    };
  },
};
</script>

<style scoped>
* {
  --gap: 1rem;
}
.container {
  background-color: palevioletred;
  display: flex;
  flex-direction: column;
  gap: var(--gap);
}
.sliderContainer {
  display: flex;
  flex-direction: column;
  gap: var(--gap);
}
</style>
