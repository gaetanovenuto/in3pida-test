<script>
import AppHeader from './components/Header/AppHeader.vue';

export default {
  data() {
    return {
      cursorX: 0,
      cursorY: 0,
    };
  },
  components: {
    AppHeader,
  },
  mounted() {
    window.addEventListener("mousemove", this.trackMouseMove);
  },
  beforeUnmount() {
    window.removeEventListener("mousemove", this.trackMouseMove);
  },
  methods: {
    trackMouseMove(e) {
      this.cursorX = e.clientX;
      this.cursorY = e.clientY;
    },
  },
}
</script>

<template>
    <div class="cursorTracker" :style="{ left: cursorX + 'px', top: cursorY + 'px'}"></div>
    <AppHeader />
    <main>
      <router-view />
    </main>
</template>

<style lang="scss">
@import "bootstrap/scss/bootstrap";
@import "./assets/scss/partials/variables.scss";

body {
  
  .cursorTracker {
    width: 15px;
    height: 15px;
    background-color: $darkBeige;
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    transform: translate(-50%, -50%);
    transition: transform 0.1s ease;
  }
}


</style>
