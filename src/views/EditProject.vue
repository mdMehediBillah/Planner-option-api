<template>
  <div class="edit-project">
    <h1>Edit Project</h1>
    <form @submit.prevent="handleEdit">
      <label>Name:</label>
      <input type="text" required placeholder="Project title" v-model="title" />
      <label>Details:</label>
      <textarea
        required
        placeholder="Describe the project"
        v-model="details"
      ></textarea>
      <button>Update project</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      url: "http://localhost:3000/projects/",
      title: "",
      details: "",
    };
  },
  mounted() {
    fetch(`${this.url}${this.$route.params.id}`)
      .then((response) => response.json())
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
      })
      .catch((error) => console.error("Error:", error));
  },
  methods: {
    handleEdit() {
      const project = {
        title: this.title,
        details: this.details,
        complete: false,
      };
      fetch(`${this.url}${this.$route.params.id}`, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(project),
      })
        .then(() => this.$router.push("/"))
        .catch((error) => console.error("Error:", error));
    },
  },
};
</script>

<style></style>
