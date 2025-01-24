<script>
import AppHeader from './components/Header/AppHeader.vue';
import AppMain from './components/Main/AppMain.vue';
import AppFooter from './components/Footer/AppFooter.vue';
import Sidebar from './components/Menu/Sidebar.vue';

export default {
  data() {
    return {
      cursorX: 0,
      cursorY: 0,
    };
  },
  components: {
    AppHeader,
    AppMain,
    AppFooter,
    Sidebar
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
    <AppMain />
    <AppFooter />
    <Sidebar />
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
