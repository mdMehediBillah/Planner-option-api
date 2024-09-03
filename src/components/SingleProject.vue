<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="action">
      <h3 @click="showDetails">{{ project.title }}</h3>
      <div class="icons">
        <!-- Action icons with event handling -->
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }"
          ><i class="fa-solid fa-pen icon"></i
        ></router-link>
        <!-- <i class="fa-solid fa-pen icon"></i> -->
        <i class="fa-solid fa-trash icon" @click="deleteProject"></i>
        <i class="fa-solid fa-check icon tick" @click="toggelComplete"></i>
      </div>
    </div>
    <div v-if="details" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      details: false,
      url: "http://localhost:3000/projects/", // Base URL for API requests
    };
  },
  methods: {
    showDetails() {
      this.details = !this.details; // Toggle project details visibility
    },
    deleteProject() {
      // Corrected URL concatenation and usage in fetch request
      fetch(`${this.url}${this.project.id}`, {
        method: "DELETE",
      })
        .then(() => this.$emit("projectDeleted", this.project.id))
        .catch((error) => console.error("Error:", error));
    },
    toggelComplete() {
      // Corrected URL concatenation and usage in fetch request
      fetch(`${this.url}${this.project.id}`, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ complete: !this.project.complete }),
      })
        .then(() => {
          this.$emit("complete", this.project.id);
        })
        .catch((error) => console.error("Error:", error));
    },
  },
};
</script>

<style scoped>
.project {
  margin: 20px auto;
  background: white;
  border-radius: 5px;
  border-left: 4px solid #e90074;
  padding: 10px 20px;
}

.project.complete {
  border-left: 4px solid #08914f;
  background: rgb(213, 229, 229);
}

h3 {
  color: rgb(7, 82, 181);
  cursor: pointer;
}

.action {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.icon {
  cursor: pointer;
  padding: 6px;
  border-radius: 50%;
  background: #fefdfd;
  color: gray;
}

.icon:hover {
  background: #d5d5d5;
  color: rgb(7, 83, 191);
}

.icons {
  display: flex;
  gap: 4px;
  align-items: center;
}
.project.complete .tick {
  color: #b4ebea;
  background: #027362;
}
</style>
