<template>
  <div class="container" :style="{'background-color': backgroundColor}">
    <h2 :ref="`currentTitle${backgroundColor}`" class="title">{{backgroundColor}}</h2>
  </div>
</template>

<script>
const offset = 400;

export default {
  name: "Container",
  props: {
    backgroundColor: String,
    currentWindowY: Number
  },
  data() {
    return {
      isCurrentSticky: false,
      startTitlePosition: 0,
      endTitlePosition: 0
    };
  },
  methods: {
    handleScroll() {
      const currentRef = this.getCurrentRef(this.backgroundColor);
      const windowPositionY = this.currentWindowY;
      if (
        this.startTitlePosition <= windowPositionY &&
        windowPositionY < this.endTitlePosition
      ) {
        currentRef.classList.add("sticky");
      } else {
        currentRef.classList.remove("sticky");
      }
    },
    getCurrentRef(backgroundColor) {
      return this.$refs[`currentTitle${backgroundColor}`];
    }
  },
  watch: {
    currentWindowY() {
      this.handleScroll();
    }
  },
  mounted() {
    const currentRef = this.getCurrentRef(this.backgroundColor);
    this.startTitlePosition = currentRef.offsetTop;
    this.endTitlePosition = this.startTitlePosition + offset;
  }
};
</script>

<style scoped>
.container {
  width: 100%;
  height: 400px;
}
.sticky {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
.title {
  color: white;
  margin: 0;
  background-color: black;
}
</style>