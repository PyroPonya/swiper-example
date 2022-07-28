<template>
  <div class="container">
    <div class="sliderTitle">
      <h2>slider {{ props.elName }}</h2>
      <a href="#"><h3>Смотреть все</h3></a>
    </div>
    <swiper
      :slides-per-view="'auto'"
      :space-between="30"
      :modules="modules"
      class="mySwiper"
    >
      <swiper-slide v-for="num in 9" :key="num"
        >Slide {{ props.elName + num }}</swiper-slide
      >
    </swiper>
  </div>
</template>
<script>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination } from 'swiper';

// Import Swiper styles
import 'swiper/css';
import 'swiper/css/pagination';

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  props: ['elName'],
  setup(props) {
    return {
      props,
      modules: [Pagination],
    };
  },
};
</script>

<style scoped>
* {
  --heingh: 15rem;
}
html,
body {
  position: relative;
  height: 100%;
}
body {
  background: #eee;
  font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 14px;
  color: #000;
  margin: 0;
  padding: 0;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.sliderTitle {
  display: flex;
  flex-direction: row;
  align-items: flex-end;
  justify-content: space-between;
  flex-wrap: nowrap;
  width: 100%;
}
.sliderTitle > h2,
h3,
a {
  margin: 0 1rem;
}
.swiper {
  width: 100%;
  height: var(--heingh);
  display: flex;
  align-items: center;
  justify-content: center;
}
.swiper-slide {
  text-align: center;
  font-size: 28px;
  background: rgb(50, 115, 168);
  height: var(--heingh);

  /* Center slide text vertically */
  display: -webkit-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  -webkit-justify-content: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  -webkit-align-items: center;
  align-items: center;
}

.swiper-slide img {
  display: block;
  width: 100%;
  height: var(--heingh);
  object-fit: cover;
}

/* placeholder. slide sizes for example */
.swiper-slide {
  width: 90%;
}

.swiper-slide:nth-child(2n) {
  width: 60%;
}

.swiper-slide:nth-child(3n) {
  width: 40%;
}
</style>
