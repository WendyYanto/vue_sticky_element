<template>
  <div class="about">
    <h1>This is an about page</h1>
    <Container
      v-for="backgroundColor in backgroundColors"
      :key="backgroundColor"
      :currentWindowY="currentWindowY"
      :backgroundColor="backgroundColor"
    />
  </div>
</template>

<script>
import Container from "./Container";

export default {
  name: "About",
  components: {
    Container
  },
  data() {
    return {
      backgroundColors: ["Red", "Blue", "Green", "Yellow", "Black"],
      currentWindowY: 0
    };
  },
  mounted() {
    window.addEventListener("scroll", this.updateCurrentWindowY);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.updateCurrentWindowY);
  },
  methods: {
    updateCurrentWindowY() {
      this.currentWindowY = window.scrollY;
    }
  }
};
</script>


