<template>
     <div class="edit-task">
        <NuxtLink to="/"><svg xmlns="http://www.w3.org/2000/svg" class="back-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
</svg></NuxtLink>
        <h2 class="heading">Edit Task</h2>
        <form class='form'>
            <label>Name:</label>
            <input type="text" v-model="task_name" required class="name-input"/>
            <br/>

            <label>Description:</label>
            <textarea v-model="task_description" class="desc-input" rows="6"></textarea>
            <br/>

            <label>Status:</label>
            <label v-if="status">{{status}}</label> 
            <select v-else v-model="task_status" class="status-input">
                <option v-for="status, i in totalStatus" :key="i" :value="status" >{{status}}</option>
            </select>
            <br/>

            <button @click="() => {
                let newTask = {
                    task: task_name, 
                    description: task_description,
                    status: task_status, 
                    id: id,
                }
                editTask({
                    task: task_name,
                    description: task_description,
                    status: task_status,
                    id: id
                })
                this.$nuxt.$options.router.push(`/`);
            }" >
                Submit
            </button>
        </form>
    </div>
</template>

<script>
    import {mapMutations} from 'vuex'
    import {mapState} from 'vuex'

    export default {
        props: ['id'],
        methods: {
            ...mapMutations(['editTask'])
        },
        computed: {
            task() {
                return this.$store.getters.getTaskById(this.id)
            },
            ...mapState(['totalStatus'])
        },
        
        data() {
            let temp = JSON.parse(localStorage.getItem('allTasks') || "[]").find(task => task.id == this.id)
            return {
                task_name: temp.task,
                task_description: temp?.description,
                task_status: temp.status,
            }
        },
    }
</script>

<style  scoped>
.edit-task {
    display: flex;
    flex-direction: column;
    margin-top: 12rem;
    border: 1px solid black;
    max-width: 200px;
    margin-left:auto;
    margin-right: auto;
    padding: 0.5rem 1rem;
}
.heading {
    text-align: center;
}
.back-icon {
    height: 15px;
    width: 15px;
}
.name-input {
    box-sizing: border-box;
    width: 100%;
    margin-top:0.4rem;
    margin-bottom: 0.4rem;
}
.desc-input {
    box-sizing: border-box;
    width: 100%;
    margin-top:0.4rem;
    margin-bottom: 0.4rem;
}
.status-input {
    box-sizing: border-box;
    width: 100%;
    margin-top:0.4rem;
    margin-bottom: 0.8rem;
}
</style>