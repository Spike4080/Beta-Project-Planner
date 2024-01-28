<template>
        <div class="project" :class="{complete:project.complete}">
            <div class="flexing">
                <div>
                    <h2 @click="showProject =! showProject">{{project.title}}</h2>
                </div>
                <div>
                    <span class="material-symbols-outlined" @click="deleteProject">
                    delete
                    </span>
                    <router-link :to="{name:'editProject',params:{id:project.id}}">
                        <span class="material-symbols-outlined">edit</span>
                    </router-link>
                    <span class="material-symbols-outlined" @click="completeProject">
                    done
                    </span>
                </div>
            </div>
            <p v-if="showProject">{{project.detail}}</p>
        </div>
</template>

<script>
export default {
    props:['project'],

    data() {
        return  {
            showProject: false,
            api: "http://localhost:3000/projects/",
        }
    },

    methods: {
        deleteProject() {
            let deleteRoute = this.api+this.project.id;
            fetch(deleteRoute,{method:"DELETE"})
            .then(()=>{
                this.$emit("delete",this.project.id)
            })
            .catch(()=>{

            })
        },
        completeProject() {
            let completeRoute = this.api+this.project.id;
            fetch(completeRoute,{
                method:"PATCH",
                headers:{
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(
                    {
                        complete:this.project.complete =! this.project.complete
                    }
                )
            })
            .then(()=>{
                this.$emit('complete',this.project.id)
            })
            .catch((err)=>{
                console.log("wrong code")
            })
        }
    }
}
</script>

<style>

  h2 {
    color: indigo;
  }

  .project {
    background: #f2f2f2;
    cursor: pointer;
    margin: 10px;
    padding: 10px;
    border-left: 8px solid crimson;
    border-radius: 10px;
  }

    .flexing {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    span {
        margin-right: 10px;
    }
    
    .complete {
        border-left-color: green;
    }

</style>