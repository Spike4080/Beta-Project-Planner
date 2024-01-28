<template>
  <div class="home">
    <h1>Hello</h1>
    <div v-for="project in projects" :key="project.id">
      <SingleProject :project="project" @delete="deleteSingleProject" @@complete="completeProject"></SingleProject>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject'
// @ is an alias to /src


export default {
  name: 'Home',
  components: {
    SingleProject,},
  data(){
    return {
      projects: [],
    }
  },
  methods:{
    deleteSingleProject(id) {
      this.projects = this.projects.filter(project=>{
        return project.id != id;
      })
    },
    completeProject(id) {
      let completeProject = this.projects.find(project=>{
        return project.id === id
      })
      completeProject.complete =! completeProject.complete;
    }
  },
  mounted(){
    fetch("http://localhost:3000/projects")
    .then((response)=>{
      return response.json();
    })
    .then((datas)=>{
      this.projects = datas
    })
    .catch((err)=>{
      console.log(err.message());
    })
  }
}
</script>
