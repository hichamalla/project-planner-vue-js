<template>
  <div class="project" :class="{complete :project.complete,deleted:project.deleted}">
    <!-- <h1>Hiiiii</h1> -->

    <div class="actions">
      <h3 @click="showDetails=!showDetails">
        {{project.title}}
      </h3>
      <div class="icons">
        <span class="material-symbols-outlined" @click="toggleDelete">
          delete
        </span>
        <RouterLink :to="{name:'EditProject',params:{id:project.id}}">
        <span class="material-symbols-outlined">
          edit
        </span>
      </RouterLink> 
        <span class="material-symbols-outlined" @click="toggleDone">
          {{project.complete==true?"done":"radio_button_checked"}}
        </span>
      </div>
    </div>

    <div class="details" v-if="showDetails"> {{project.details}}</div>
  </div>
</template>

<script>
import axios from 'axios';


export default {
  name: 'SingleProject',
  props: ['project'],
  data() {
    return {
      showDetails: false,
      uri: 'http://localhost:3000/projects/' + this.project.id
    }
  },
  methods: {
    toggleDone() {
      // console.log(this.uri);
      // this.project.complete=!this.project.complete 
      axios.patch(this.uri,
        {
          complete: !this.project.complete
        }
        ,)
        .then(() => {
          console.log('done'),
            this.$emit('complete', this.project.id)
        })
        // .then(response => console.log(response.data))
        .catch(err => {
          console.log('errCompleted'),
            console.log(err)
        })
    },
    toggleDelete() {
      // console.log(this.uri);
      // this.project.complete=!this.project.complete 
      axios.patch(this.uri,
        {
          deleted: true
        }
        ,)
        .then(() => {
          console.log('deleted'),
            this.$emit('deleted', this.project.id)
        })
        // .then(response => console.log(response.data))
        .catch(err => {
          console.log('errDelete'),
            console.log(err)
        })
    }
  }
}
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
}

h3 {
  cursor: pointer;
}

.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}

.material-icons:hover {
  color: #777;
}

/* completed projects */
.project.complete {
  border-left: 4px solid #00ce89;
}

.project.complete .tick {
  color: #00ce89;
}
</style>