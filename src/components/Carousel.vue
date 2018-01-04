<template>
  <div class="carousel">
    <CarouselSlide v-for="n in slides" :index="n - 1">
      <img :src="'http://lorempicsum.com/simpsons/600/304/' + n" width="100%">
    </CarouselSlide>
    <button @click="PrevSlide" class="btn-prev">Prev</button>
    <button @click="NextSlide" class="btn-next">Next</button>
    <div class="pagination">
      <button v-for="n in slides" @click="goto(n - 1)" :class="{active: n-1 == currentIndex}">{{ n }}</button>
    </div>
  </div>
</template>

<script>
import CarouselSlide from './CarouselSlide'

export default {
  components: {
    CarouselSlide
  },
  data () {
    return {
      currentIndex: 0,
      slides: 5,
      seconds: 0,
      direction: 'right'
    }
  },
  computed: {
    slidesCount () {
      return this.slides
    }
  },
  methods: {
    PrevSlide () {
      this.currentIndex--
      this.direction = 'left'
      this.seconds = 0
      if(this.currentIndex < 0) {
        this.currentIndex = this.slidesCount - 1
        this.direction = 'right'
      }
    },
    NextSlide () {
      this.currentIndex++
      this.direction = 'right'
      this.seconds = 0
      if(this.currentIndex >= this.slidesCount) {
        this.currentIndex = 0
        this.direction = 'left'
      }
    },
    goto (index) {
      this.direction = this.currentIndex >= index ? 'left' : 'right'
      this.currentIndex = index
      this.seconds = 0
    }
  },
  mounted () {
    setInterval(() => {
      this.seconds++
      if(this.seconds >= 5) {
        this.NextSlide()
        this.seconds = 0
      }
    }, 1000)
  }
}
</script>

<style>
  button {
    border: none;
    padding: 5px 10px;
    cursor: pointer;
  }
  button.active {
    background-color: #000;
    color: #FFF;
  }
  div.carousel {
    width: 600px;
    height: 304px;
    margin: 0 auto;
    position: relative;
    overflow: hidden;
  }

  button.btn-prev {
    left: 15px;
    top: calc(50% - 10.5px);
    position: absolute;
  }

  button.btn-next {
    right: 15px;
    top: calc(50% - 10.5px);
    position: absolute;
  }

  .pagination {
    position: absolute;
    bottom: 20px;
    left: 0;
    right: 0;
    text-align: center;
  }
</style>