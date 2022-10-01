<template>
  <div class="home">
    <FilterNav current="all" @filterBy="handleChangeFilter"></FilterNav>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <!-- {{project.title}} -->
        <SingleProject :project="project" @complete="HandleCompleted" @deleted="handleDelete"></SingleProject>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'


// import TheWelcome from "../components/TheWelcome.vue";
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue";


export default {
  components: { SingleProject, FilterNav },
  data() {
    return {
      currentFilter: 'all',
      projects: [],

    };
  },

  mounted() {
    axios
      .get('http://localhost:3000/projects')
      .then(response => {
        // console.log("response.data")

        this.projects = response.data
        // .filter(project=>{
        //   // console.log(project.deleted)
        //   return (project.deleted==false || typeof (project.deleted) === 'undefined')
        // })
        // handlefilter()
      })

  },
  methods: {
    HandleCompleted(id) {
      let p = this.projects.find(project => project.id === id)
      p.complete = !p.complete
    },
    handleDelete(id) {
      this.projects = this.projects.filter(project => {
        project.id === id ? project.deleted = true : ''
        return project.id !== id
      })
    },
    handleChangeFilter(current) {
      console.log('handleChangeFilter')
      console.log(current)
      this.currentFilter = current
    }

  },
  computed: {
    filteredProjects() {
      console.log('ee')
      console.log(this.projects)
      if (this.currentFilter === 'completed') {
        return this.projects.filter(project=>project.complete&&!project.deleted)
      }
      if (this.currentFilter === 'ongoing') {
        return this.projects.filter(project=>!project.complete&&!project.deleted)
      }
      if (this.currentFilter == "deleted") {
        return this.projects.filter(project=>project.deleted)
      }
      return this.projects
    }
    //  .filter(project=>project.deleted=false)
  }

}
</script>