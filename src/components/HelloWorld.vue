<template>
  <div class="hello">
    <Slick
      ref="slick"
      @afterChange="handleAfterChange"
      @beforeChange="handleBeforeChange"
      @breakpoint="handleBreakpoint"
      @destroy="handleDestroy"
      @edge="handleEdge"
      @reInit="handleReInit"
      @setPosition="handleSetPosition"
      @swipe="handleSwipe"
      @lazyLoaded="handleLazyLoaded"
      @lazyLoadError="handleLazeLoadError"
    >
      <div class="box1" v-if="obj.box1"></div>
      <div class="box2" v-if="obj.box2"></div>
      <div class="box3" v-if="obj.box3"></div>
    </Slick>
  </div>
</template>

<script>
import Slick from "vue-slick";
import "../assets/style.css";
export default {
  components: { Slick },
  props: {
    msg: String
  },
  data() {
    return {
      obj: { box1: true, box2: true, box3: true }
    };
  },
  mounted() {
    this.obj.box1 = true;
    this.obj.box2 = false;
    this.obj.box3 = true;
    this.reInit();
  },
  methods: {
    next() {
      this.$refs.slick.next();
    },

    prev() {
      this.$refs.slick.prev();
    },

    reInit() {
      // Helpful if you have to deal with v-for to update dynamic lists
      this.$nextTick(() => {
        this.$refs.slick.reSlick();
      });
    },

    // Events listeners
    handleAfterChange(event, slick, currentSlide) {},
    handleBeforeChange(event, slick, currentSlide, nextSlide) {},
    handleBreakpoint(event, slick, breakpoint) {},
    handleDestroy(event, slick) {},
    handleEdge(event, slick, direction) {},

    handleReInit(event, slick) {
      console.log("handleReInit", event, slick);
    },
    handleSetPosition(event, slick) {},
    handleSwipe(event, slick, direction) {},
    handleLazyLoaded(event, slick, image, imageSource) {},
    handleLazeLoadError(event, slick, image, imageSource) {}
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  width: 100%;
  height: 200px;
  border: 1px solid #000;
}
.box1 {
  width: 100%;
  height: 200px;
  background: red;
}
.box2 {
  height: 200px;
  width: 100%;
  background: yellow;
}
.box3 {
  height: 200px;
  width: 100%;
  background: blue;
}
</style>
