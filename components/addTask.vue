<template>
    <div class="edit-task">
        <NuxtLink to="/"><svg xmlns="http://www.w3.org/2000/svg" class="back-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
</svg></NuxtLink>
        <h2 class="heading">Add a Task</h2>
        <form class='form'>
            <label>Name:</label>
            <input type="text" v-model="task_name" required class="name-input"/>
            <br/>

            <label>Description:</label>
            <textarea v-model="task_description" class="desc-input" rows="6"></textarea>
            <br/>

            <label>Status:</label>
            <label v-if="status">{{status}}</label> 
            <select v-else v-model="task_status">
                <option value="status" >Status</option>
            </select>
            <br/>

            <button @click="() => {
                addTask({
                    task: task_name,
                    description: task_description,
                    status: status,
                    id: Math.floor((Math.random() * 100) + 1)
                })

                this.$nuxt.$options.router.push(`/`);
            }" class="submit-btn">
                Submit
            </button>
        </form>
    </div>
</template>

<script>
    import {mapMutations} from 'vuex'
    export default {
        props: ['status'],
        data() {
            return {
                task_name: "",
                task_description: ""
            }
        },
        methods: {
            ...mapMutations(['addTask'])
        }
    }
</script>

<style scoped>
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
.submit-btn {
    margin-top:0.8rem;
}
</style>