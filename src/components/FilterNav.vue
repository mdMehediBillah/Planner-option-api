<template>
  <nav class="filter-nav">
    <button
      @click="filterProjects('all')"
      :class="{ active: current === 'all' }"
    >
      View All
    </button>
    <button
      @click="filterProjects('completed')"
      :class="{ active: current === 'completed' }"
    >
      Completed
    </button>
    <button
      @click="filterProjects('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"], // Correctly defined props
  methods: {
    filterProjects(by) {
      this.$emit("filterChange", by); // Emit filter change event
    },
  },
};
</script>

<style>
.filter-nav {
  display: flex;
  justify-content: center;
  margin: 0.2rem 0;
}
.filter-nav button {
  color: rgb(133, 131, 190);
  border: none;
  border-radius: 5px;
  padding: 0.5rem 1rem;
  /* margin: 0 0.2rem; */
  cursor: pointer;
}
.filter-nav button.active {
  /* background: rgb(147, 4, 128); */
  color: rgb(132, 6, 55);
  font-weight: bold;
}
</style>
