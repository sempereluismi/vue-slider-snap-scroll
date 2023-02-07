<template>
  <div class="slider" ref="slider">
    <div class="slider__controls left">
      <a @click="moveSlider(1)" href="#" class="slider__controls__link"> 1 </a>
    </div>
    <img v-for="(slide, index) in slides" :key="index" :src="slide" class="slider__content">
    <div class="slider__controls right">
      <a @click="moveSlider(2)" href="#" class="slider__controls__link"> 2 </a>
    </div>
  </div>

</template>

<script>
export default {
  name: "AppSlider",
  mounted() {
    this.slider = this.$refs.slider;
    this.height = this.slider.offsetHeight;
    this.Width = this.slider.offsetWidth;

  },
  props: {
    slides: {
      type: Array,
      required: true,
    }
  },
  data() {
    return {
      slider: null,
      height: null,
      Width: null,
      count: 0
    };
  },
  methods: {
    moveSlider(n) {
      if (n == 1) {
        console.log(this.count * this.Width)
        this.count--
        if( this.count < 0 ) this.count = 0;

        this.slider.scrollTo({
          left: this.count * this.Width,
          top: this.height,
          behavior: 'smooth'
        })
        
      } else { 
        this.count++
        if( this.count > this.slides.length ) this.count = this.slides.length-1
        console.log(this.Width * this.count)
        this.slider.scrollTo({
          left: this.Width * this.count,
          top: this.height,
          behavior: 'smooth'
        })
      }
    }
  }
};
</script>

<style>
.slider {
  display: flex;

  width: 100%;
  height: 100vh;

  scroll-snap-type: x mandatory;

  overflow-x: scroll;
  overflow-y: hidden;
}

.slider img {
  flex: 0 0 100%;
  width: 100%;
  object-fit: cover;

  scroll-snap-align: center;
}

.slider__controls {
  position: fixed;
  top: 0;
  width: 3rem;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.right {
  right: 0.5rem;
}

.left {
  left: 0.5rem;
}

.slider__controls__link {
  width: 3rem;
  height: 3rem;
  background-color: rgba(255, 255, 255, .8);
  color: black;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  text-decoration: none;
  font-weight: bold;
  margin: 1rem 0;
}
</style>
