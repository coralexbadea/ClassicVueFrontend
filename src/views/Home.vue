<template>

    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks
      @toggle-reminder="toggleTask"
      @delete-task="deleteTask" :tasks="tasks"
      @edit-task="editTask" />
 
</template>


<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'
export default {
    name: "Home",
    props: {
        showAddTask: Boolean
    },
    components: {
        Tasks,
        AddTask,
    },
    data(){
        return{
            tasks: [],
        }
    },
    methods:{
        addTask(task){
            this.tasks = [...this.tasks, task]
        },
        async deleteTask(id){
            if(confirm('Are you sure?')){
                const res = await fetch(`api/tasks/${id}`, {
                method: "DELETE",
                })

                res.status === 200 ? (this.tasks = this.tasks.filter((task)=>task.id !== id))
                                    : alert("Error deleting task")
            }
        },
        async toggleTask(id){
            const taskToToogle = await this.fetchTask(id)
            const updTask = {...taskToToogle, reminder: !taskToToogle.reminder}

            const res = await fetch(`api/tasks/${id}`, {
                method: "PUT",
                headers: {
                "Content-type": "application/json"
                },
                body: JSON.stringify(updTask)
            })

            const data = await res.json()

            this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder} : task)
        },
        async addTask(task){
            const res = await fetch('api/tasks', {
                method: "POST",
                headers: {
                'Content-type': 'application/json',
                },
                body: JSON.stringify(task)
            })
            const data = await res.json()

            this.tasks = [...this.tasks, data]

        },
        async fetchTasks() {
            const res = await fetch("api/tasks")
            const data = await res.json()
            return data
            },
            async fetchTask(id) {
            const res = await fetch(`api/tasks/${id}`)
            const data = await res.json()
            return data
        },
        async editTask(task){
            const res = await fetch(`api/tasks/${task.id}`, {
            method: "PUT",
            headers: {
            "Content-type": "application/json"
            },
            body: JSON.stringify(task)
            })

            const data = await res.json()
            this.tasks = await this.fetchTasks()
        }
    
    },
    async created() {
        this.tasks = await this.fetchTasks()
    }
}
</script>