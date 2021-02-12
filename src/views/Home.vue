<template>
  <div class="home">
    <FilterNav
      @filterChange="filterProjects($event)"
      :currentFilter="currentFilter.value"
    />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject";
import FilterNav from "../components/FilterNav";
import { computed, onMounted, ref } from "vue";

export default {
  name: "Home",
  components: {
    SingleProject,
    FilterNav,
  },
  setup() {
    const currentFilter = ref("all");
    const projects = ref([]);

    const filterProjects = (event) => {
      currentFilter.value = event
    }

    onMounted(() => {
      fetch("http://localhost:3000/projects")
        .then((res) => res.json())
        .then((data) => (projects.value = data))
        .catch((err) => console.log(err.message));
    });

    const handleDelete = (id) => {
      projects.value = projects.value.filter((project) => project.id !== id);
    };

    const handleComplete = (id) => {
      let selectedProject = projects.value.find((project) => project.id === id);

      selectedProject.complete = !selectedProject.complete;
    };

    const filteredProjects = computed(() => {
      if (currentFilter.value === "completed") {
        return projects.value.filter((project) => project.complete);
      }

      if (currentFilter.value === "ongoing") {
        return projects.value.filter((project) => !project.complete);
      }

      return projects.value;
    });

    return { projects, currentFilter, handleDelete, handleComplete, filteredProjects, filterProjects };
  },
};
</script>
