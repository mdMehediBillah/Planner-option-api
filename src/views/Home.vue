<template>
  <div class="home">
    <!-- Use method to handle filter change -->
    <FilterNav @filterChange="handleFilterChange" :current="current" />
    <div v-if="filteredProjects.length">
      <h1>Projects</h1>
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @projectDeleted="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
    <div v-else>
      <div>Loading...</div>
    </div>
  </div>
</template>

<script>
import FilterNav from "../components/FilterNav.vue";
import SingleProject from "../components/SingleProject.vue";

export default {
  name: "Home",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: "all", // Track the current filter
    };
  },
  computed: {
    // Filtered projects based on the current filter
    filteredProjects() {
      if (this.current === "all") return this.projects;
      if (this.current === "completed")
        return this.projects.filter((project) => project.complete);
      if (this.current === "ongoing")
        return this.projects.filter((project) => !project.complete);
      return this.projects;
    },
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((response) => response.json())
      .then((data) => (this.projects = data))
      .catch((error) => console.error("Error:", error));
  },
  methods: {
    handleFilterChange(filter) {
      this.current = filter; // Correctly update the current filter
    },
    handleDelete(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleComplete(id) {
      let project = this.projects.find((project) => project.id === id);
      project.complete = !project.complete;
    },
  },
};
</script>

<style>
/* Add your custom styles here */
</style>
