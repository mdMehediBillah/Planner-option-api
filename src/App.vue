<script setup></script>

<template>
  <div>
    <Navbar />
    <router-view />
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";

export default {
  name: "App",
  components: { Navbar },
};
</script>

<style scoped>
h1 {
  color: rgb(13, 82, 122);
  text-align: center;
}
</style>
