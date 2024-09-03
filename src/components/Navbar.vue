<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'Home' }">Projects</router-link>
    <router-link :to="{ name: 'AddProject' }">Add a New Project</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  color: rgb(13, 82, 122);
  margin: 0 10px;
  font-size: 1rem;
}
.main-nav a:hover {
  color: rgb(149, 6, 111);
}
a.router-link-active {
  color: rgb(30, 149, 196);
  border-bottom: 3px solid rgb(30, 149, 196);
  padding-bottom: 4px;
  font-weight: bold;
}
</style>
