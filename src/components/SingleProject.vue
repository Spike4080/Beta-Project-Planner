<template>
        <div class="project">
            <div class="flexing">
                <div>
                    <h2 @click="showProject =! showProject">{{project.title}}</h2>
                </div>
                <div>
                    <span class="material-symbols-outlined" @click="deleteProject">
                    delete
                    </span>
                    <span class="material-symbols-outlined">
                    edit
                    </span>
                    <span class="material-symbols-outlined">
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

    span:nth-child(1) {
        color: crimson;
    }

    span:nth-child(2) {
        color: blue;
    }

    span:nth-child(3) {
        color: green;
    }

</style>