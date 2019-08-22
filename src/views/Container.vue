<template>
  <div class="container" :style="{'background-color': backgroundColor}">
    <h2
      :ref="'currentTitle' + backgroundColor"
      :style="{'color': 'white','margin': '0', 'background-color': 'black'}"
    >{{backgroundColor}}</h2>
  </div>
</template>

<script>
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
      if (this.startTitlePosition <= windowPositionY && windowPositionY < this.endTitlePosition) {
        currentRef.classList.add("sticky");
      } else {
        currentRef.classList.remove("sticky");
      }
    },
    getCurrentRef(backgroundColor) {
      return this.$refs[`currentTitle${backgroundColor}`]
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
    this.endTitlePosition = this.startTitlePosition + 400;
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
</style>