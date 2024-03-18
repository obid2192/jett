<template lang="">
  <div class="container">
    <Navbar />
    <router-view />
  </div>
</template>
<script>
import Navbar from "./components/Navbar.vue";
export default {
  components: {
    Navbar,
  },
};
</script>
<style scoped>
.container{
  max-width: 1536px;
  padding: 15px;
    background-color: rgb(255, 255, 255);
    margin: auto;
    margin-top: 10px;
}
</style>
