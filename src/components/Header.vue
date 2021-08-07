<template>
    <header>
        <h1>{{title}}</h1>
    </header>
    <Button v-show="homePage" @btn-click="$emit('btn-click')" 
        :text="showAddTask ? 'Close' : 'Add Task'" color="green"/>
</template>


<script>
import Button from './Button'


export default {
    name: 'Header',
    props: {
        title: {
            type: String,
            default: 'Hello world'
        },
        showAddTask: Boolean,
    },
    components: {
        Button
    },
    computed:{
        homePage(){
            return (this.$route.path === '/')
        }
    },
    emits:['btn-click']
}
</script>

<style scoped>
    header {
        display:flex;
        align-items:center;
        justify-content: space-between;
        margin-bottom: 20px;
    }
</style>