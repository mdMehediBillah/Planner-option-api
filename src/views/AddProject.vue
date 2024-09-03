<template>
  <div>
    <h1 class="addProjectTitle">Add Project</h1>
    <form @submit.prevent="handleSubmit">
      <label>Name:</label>
      <input type="text" required placeholder="Project title" v-model="title" />
      <label>Details:</label>
      <textarea
        required
        placeholder="Describe the project"
        v-model="details"
      ></textarea>
      <button>Add Project</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      url: "http://localhost:3000/projects/",
      title: "",
      details: "",
    };
  },
  methods: {
    handleSubmit() {
      const project = {
        title: this.title,
        details: this.details,
        complete: false,
      };
      fetch(this.url, {
        method: "POST",
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

<style>
form {
  background: white;
  padding: 20px;
  border-radius: 20px;
}
label {
  display: block;
  margin: 20px 0 10px 0;
  letter-spacing: 1px;
  text-transform: uppercase;
  font-size: 0.8rem;
  font-weight: bold;
  color: #bbb;
}
input {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-sizing: border-box;
}
textarea {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-sizing: border-box;
}
form button {
  display: block;
  margin: 20px auto 0;
  padding: 10px 40px;
  background: #0d527a;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.3s;
}
form button:hover {
  background: #ab04ae;
}
.addProjectTitle {
  color: rgb(13, 82, 122);
  text-align: center;
}
</style>
