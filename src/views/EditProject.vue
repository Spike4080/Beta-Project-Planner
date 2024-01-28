<template>
  <h1>Edit</h1>
    <form @submit.prevent="addProject">
        <label>Project Title</label>
        <input type="text" v-model="title">
        <label>Project Detail</label>
        <input type="text" v-model="detail">
    <button @click="editProject">Update Project</button>
  </form>
</template>

<script>
export default {
    props:['id'],
    data() {
        return {
            title: "",
            detail: ""
        }
    },

    mounted() {
        fetch('http://localhost:3000/projects/'+this.id)
        .then((res)=>{
            return res.json()
        })
        .then((datas)=>{
            this.title = datas.title,
            this.detail = datas.detail
        })
        .catch((err)=>{
            console.log(err)
        })
    },
    methods: {
        editProject() {
            fetch('http://localhost:3000/projects/'+this.id,{
                method:'PATCH',
                headers:{"Content-Type":"application/json"},
                body:JSON.stringify(
                    {
                        title:this.title,
                        detail:this.detail
                    }
                )
                })
            .then(()=>{
                this.$router.push("/")
            })
            .catch(()=>{
                console.log(err)
            })
        }
    }
}
</script>

<style>

</style>