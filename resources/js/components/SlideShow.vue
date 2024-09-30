<template>
  <div class="component-container">
    <swiper
      class="swiper"
      :options="swiperOption"
      @init="initialise"
      @slideChange="slideChange"
    >
      <swiper-slide
        v-for="(img, index) in images"
        :key="index"
        :class="currentIndex == index ? 'active-card' : ''"
      >
        <div class="swiper-zoom-container">
          <img :src="img" />
        </div>
      </swiper-slide>
    </swiper>
    <div class="nav">
      <div class="swiper-button-prev" slot="button-prev"></div>
      <div class="swiper-button-next" slot="button-next"></div>
    </div>
  </div>
</template>

<script>
// import { Swiper, SwiperSlide } from "vue-awesome-swiper";
import { Swiper, SwiperSlide } from "swiper/vue";

////////using swiper6
// import "swiper/swiper-bundle.min.css";
// import "swiper/components/effect-coverflow/effect-coverflow.min.css";

///////using swiper7, 8
import 'swiper/css/bundle'
import 'swiper/css/effect-coverflow'

import 'swiper/css'

import SwiperCore, { EffectCoverflow, Navigation } from "swiper/core";
// SwiperCore.use([EffectCoverflow, Navigation]);

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  data() {
    return {
      swiperOption: {
        effect: "coverflow",
        grabCursor: true,
        centeredSlides: true,
        slidesPerView: "auto",
        loop: true,
        coverflowEffect: {
          rotate: 0,
          stretch: -80,
          depth: 300,
          modifier: 1,
          slideShadows: true,
        },
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
        modules: [ EffectCoverflow, Navigation ],
        // wrapperClass: "swiper-wrapper",
      },
      currentIndex: 0,
      images: [
        "/images/example/1.png",
        "/images/example/2.png",
        "/images/example/3.png",
      ],
    };
  },
  methods: {
    initialise() {
      console.log("init");
    },
    slideChange(event) {
      this.currentIndex = event.realIndex;
      console.log("slideChange", this.currentIndex);
    },
  },
};
</script>

<style lang="scss" scoped>
.nav {
  margin-top: 100px;
}

.component-container {
  width: 100%;
  height: 400px;
  padding-top: 50px;
  padding-bottom: 50px;
}

.swiper {
  height: 100%;
  width: 100%;

  .swiper-slide {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 300px;
    height: 300px;
    background-position: center;
    background-size: cover;
    color: white;
  }
}
.active-card {
  border: 1px solid black;
}
img {
  height: 300px;
  width: 300px;
}
</style>
