<template>
 <div v-for="task in tasks" :key="task.id">
     <Task @toggle-reminder="$emit('toggle-reminder', task.id)" 
            @delete-task="$emit('delete-task', task.id)" 
            @set-task-to-edit="setTaskToEdit"
            :task="task" />
     <EditTask v-show="taskToEdit==task.id" @edit-task="onEditTask" :task="task" />
 </div>   
</template>


<script>
import Task from "./Task"
import EditTask from "./EditTask"
export default {
    name:"Tasks",
    data(){
        return{
            taskToEdit: -1
        }
    },
    props: {
        tasks: Array,
    },
    components:{
        Task,
        EditTask,
    },
    methods:{
        onEditTask(task){
            this.setTaskToEdit(task.id)
            this.$emit('edit-task', task)
        },
        setTaskToEdit(id){
            this.taskToEdit = (this.taskToEdit == id) ? -1 : id
        }
    },
    emits: ['delete-task', 'toggle-reminder', 'edit-task']
}
</script>