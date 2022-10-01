<template>
    <form @submit.prevent="updateData">
      <div v-if="errors" @click="errors=!errors">
      <span style="color:red">error:</span>
      <div>{{errorMsg}}</div>
    </div>
        <label>Title</label>
        <input type="text" v-model="project.title" >
        <label>Details</label>
        <textarea v-model="project.details"></textarea>
        
        <input type="checkbox" id="checkbox" v-model="project.complete">
        <label for="checkbox">Completed</label>
        <button>Create</button>
    </form>
</template>
<script>
import axios from 'axios'


export default {
    name: "EditProject",
    props:['id'],
    data(){
        return{
          errors:false,
          errorMsg:"",
            project:{
            idw:10000,
            title:'',
            details:'',
            deleted:false,
            complete:false,
            },
            uri:'http://localhost:3000/projects/'+this.id
        }
    },
    mounted(){
      axios.get(this.uri)
      .then(response=>{
        // console.log(response)
        this.project.title=response.data.title
        this.project.details=response.data.details
        this.project.deleted=response.data.deleted
        this.project.complete=response.data.complete
      })
    },
    methods:{
        updateData() {
            // console.log(this.project)
            axios.patch(this.uri+1,this.project)
            .then(response=>console.log(response))
            .catch(err=>{
              // console.log(err.message)
              this.errors=true
            this.errorMsg=err.message}
            )
        }
    },
    
}
</script>
<style>
     form {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }
  label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0
  }
  input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
  }
  form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
  }
</style>