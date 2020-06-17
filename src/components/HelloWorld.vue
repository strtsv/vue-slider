<template>
  <div class="container">
    <div @mouseenter="stop" @mouseleave="play">
      <div ref="slider" class="slider swipe">
        <div class="swipe-wrap">
          <div v-for="index in items" :key="index.id">
            <div>
              <div class="index">{{ index }}</div>
              <picture>
                <source
                  media="(min-width: 980px)"
                  :srcset="
                    'https://gorky.media/wp-content/uploads/2020/06/image-from-rawpixel-id-2328773-jpeg.gif'
                  "
                />
                <source
                  media="(min-width: 481px)"
                  :srcset="
                    'https://gorky.media/wp-content/uploads/2020/06/web-23.jpg'
                  "
                />
                <img
                  src="https://gorky.media/wp-content/uploads/2020/06/web-17.jpg"
                  alt=""
                  class="slider__image"
                />
              </picture>
            </div>
          </div>
        </div>
      </div>
      <div class="pag">
        <div
          v-for="pag in items" :key="pag.id"
          @click="goTo(pag - 1)"
          :class="{ active: activeIndex == pag }"
        >
          {{ pag }}
        </div>
      </div>
      <div class="prev" @click="prev">назад</div>
      <div class="next" @click="next">вперед</div>
    </div>
  </div>
</template>

<script>
import Swipe from "swipejs";

export default {
  name: "HelloWorld",
  data() {
    return {
      slider: null,
      items: 4,
      activeIndex: 1,
    };
  },
  mounted() {
    const vm = this;
    this.slider = new Swipe(this.$refs["slider"], {
      startSlide: 0,
      speed: 400,
      auto: 3000,
      draggable: false,
      continuous: true,
      disableScroll: true,
      stopPropagation: false,
      callback: function(index) {
        vm.activeIndex = index + 1;
      },
      transitionEnd: function() {},
    });
  },
  methods: {
    play() {
      this.slider.restart();
    },
    stop() {
      this.slider.stop();
    },
    prev() {
      this.slider.prev();
    },
    next() {
      this.slider.next();
    },
    goTo(index) {
      this.slider.slide(index);
    },
  },
};
</script>
<style>
.index {
  position: absolute;
  left: 50%;
  top: 50%;
  z-index: 3;
  color: red;
  font-size: 30px;
  font-weight: bold;
  transform: translate3d(-50%, -50%, 0);
}
.container {
  max-width: 1176px;
  margin: 0 auto;
}

.slider {
  position: relative;
}

.slider__image {
  max-width: 100%;
  display: block;
}

.swipe {
  overflow: hidden;
  /*visibility: hidden;*/
  position: relative;
}
.swipe-wrap {
  overflow: hidden;
  position: relative;
}
.swipe-wrap > div {
  float: left;
  width: 100%;
  position: relative;
  overflow: hidden;
}

.pag {
  display: flex;
  justify-content: center;
  margin: 10px 0;
}

.pag div {
  width: 20px;
  height: 20px;
  background: #fff;
  border: 1px solid #ccc;
  border-radius: 50%;
  font-size: 7px;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #000;
  margin: 0 5px;
}

.pag div.active {
  background: #ccc;
}

.prev,
.next {
  display: inline-block;
  padding: 10px;
  cursor: pointer;
  background: #ccc;
  color: #000;
  margin: 10px;
}
</style>
