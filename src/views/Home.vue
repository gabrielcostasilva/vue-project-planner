<template>
  <div class="home">
    <FilterNav @filterChange="currentFilter = $event" :currentFilter="currentFilter" />
      <div v-if="projects.length">
        <div v-for="project in filteredProjects" :key="project.id">
          <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
        </div>
      </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject'
import FilterNav from '../components/FilterNav'

export default {
  name: 'Home',
  components: {
    SingleProject,
    FilterNav
  },
  data() {
    return {
      projects: [],
      currentFilter: 'all'
    };
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter(project => project.id !== id)
    },
    handleComplete(id) {
      let selectedProject = this.projects.find(project => project.id === id)

      selectedProject.complete = !selectedProject.complete
    }
  },
  computed: {
    filteredProjects() {
      if (this.currentFilter === 'completed') {
        return this.projects.filter(project => project.complete)
      } 

      if (this.currentFilter === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      } 

      return this.projects
    }
  }
}
</script>
