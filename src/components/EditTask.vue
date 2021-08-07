<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" v-model="task.text" name="text"/>
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text"
        v-model="task.day"
        name="day"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="task.reminder" name="reminder"/>
    </div>

    <input type="submit" value="Save Edit" class="btn" />
  </form>
</template>

<script>
export default {
    name:"EditTask",
    props:{
        task: Object
    },
    methods: {
        onSubmit(e) {
            e.preventDefault()
            if(!this.task.text) {
                alert("please add a task")
                return
            }
            this.$emit('edit-task', this.task)

        }
    },
    emits: ['edit-task']
}
</script>


<style scoped>
.add-form {
  margin-bottom: 10px;
}
.form-control {
  margin: 10px 20px;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 30px;
  margin: 5px auto;
  padding: 3px 7px;
  font-size: 15px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}

.btn{
    margin:5px 20px;
}


</style>