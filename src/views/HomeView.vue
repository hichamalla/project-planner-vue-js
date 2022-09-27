

<template>
  <div>

  </div>
  <div v-if="projects">
    <div v-for="project in projects" :key="project.id">
      <!-- {{project.title}} -->
      <SingleProject :project="project" @complete="HandleCompleted"></SingleProject>
    </div>
  </div>

</template>
<script>
import axios from 'axios'

// import TheWelcome from "../components/TheWelcome.vue";
import SingleProject from "../components/SingleProject.vue";

export default {
  components: { SingleProject },
  data() {
    return {
      projects: []
    };
  },
  mounted() {
    axios
      .get('http://localhost:3000/projects')
      .then(response => {
        // console.log("response.data")
        // console.log(response.data)
        this.projects = response.data
      })
  },
  methods: {
    HandleCompleted(id) {
      let p = this.projects.find(project => project.id === id)
      p.complete = !p.complete
    }
  }
}
</script>