<template>
  <div class="home">
    <h1>Hello</h1>
    <FilterNav @filterValue="current=$event" :current="current"></FilterNav>
    <div v-for="project in filteredProject" :key="project.id">
      <SingleProject :project="project" @delete="deleteSingleProject" @@complete="completeProject"></SingleProject>
    </div>
  </div>
  {{current}}
</template>

<script>
import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
// @ is an alias to /src


export default {
  name: 'Home',
  components: {
    FilterNav,
    SingleProject,},
  data(){
    return {
      projects: [],
      current: "all"
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
  computed:{
    filteredProject() {
      if(this.current === "complete"){
        return this.projects.filter(project=>{
          return project.complete
        })
      }
      if(this.current === "ongoing"){
        return this.projects.filter(project=>{
          return !project.complete
        })
      }
      return this.projects;
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
