<template>
  <h1>Add Project</h1>
  <form @submit.prevent="addProject">
    <label>Project Title</label>
    <input type="text" v-model="title">
    <label>Project Detail</label>
    <input type="text" v-model="detail">
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
    data(){
        return {
            title:"",
            detail:""
        }
    },
    methods: {
        addProject(){
            fetch("http://localhost:3000/projects",{
                method:"POST",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        title:this.title,
                        detail:this.detail,
                        complete:false
                    }
                )
                })
            .then(()=>{
                this.$router.push('/')
            })
            .catch((err)=>{
                console.log(err)
            })
        }
    }
}
</script>

<style>
    form {
        background: #fff;
        padding: 20px;
        border-radius: 10px;;
    }

    label {
        display: block;
        color: #bbb;
        text-transform: uppercase;
        font-weight: bold;
        letter-spacing: 1px;
        font-size: 14px;
        margin: 20px 0 10px 0;
    }

    input {
        padding: 10px;
        border: 0;
        border-bottom: 1px solid #bbb;
        box-sizing: border-box;
        width: 100%;
    }

    form button {
        display: block;
        margin: 20px auto 0;
        background: #00ce89;
        color: #fff;
        padding: 10px;
        border: 0;
        border-radius: 6px;
        font-size: 16px;
    }
</style>