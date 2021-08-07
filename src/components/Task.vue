<template>
    <div @dblclick="$emit('toggle-reminder', task.id)"  :class="[task.reminder ? 'reminder' : '', 'task']">
        <span>
            <h3>
              {{task.text}}
            </h3>
            <i @click="onDelete(task.id)" class="fas fa-times"></i>
        </span>
        
        <span>
            {{task.day}}
            <i @dblclick.stop @click.prevent="$emit('set-task-to-edit', task.id)" class="fas fa-edit"></i>
        </span>
    </div>
</template>


<script>
export default {
    name: "Tasks",
    props:{
        task: Object
    },
    methods: {
        onDelete(id){
            this.$emit('delete-task', id)
        }
    },
    emits: ['delete-task','toggle-reminder','set-task-to-edit']
}
</script>


<style scoped>
.fa-times {
  color: red;
  font-size:1.1rem
}

.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
  user-select: none;
}
.task.reminder {
  border-left: 5px solid green;
}
.task span {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin:6px;
}
</style>
