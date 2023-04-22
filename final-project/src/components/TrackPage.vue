<template>
  <div class="track-view container d-flex flex-column justify-content-center align-items-center">
    <h1 class="text-center mb-5">Track KOAT</h1>
    <div class="compass-arrow" :style="arrowStyle"></div>
    <br>
    <h2>X feet away</h2>   
  </div>
</template>

<script>
// import locations from './FindPage.vue'

export default {
  name: 'TrackPage',
  data() {
    return {
      heading: null,
    };
  },
  computed: {
    arrowStyle() {
      return {
        transform: `rotate(${this.heading}deg)`,
        width: '50',
        height: '50',
        borderStyle: 'solid',
        borderWidth: '0 80px 120px 80px',
        borderColor: `transparent transparent #007bff transparent`,
      };
    },
  }
};
</script>

<style scoped>
.track-view {
  background-color: white;
  color: #007bff;
  height: 100vh;
}
</style>
