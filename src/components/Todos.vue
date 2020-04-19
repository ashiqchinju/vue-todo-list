<template>
    <div>
        <!-- "v-for" directive is used to loop through a directive..here props is an array so.. --> 
        <!-- we need a unique key when we loop through an array so we've used "v-bind:key" here-->
        <div v-bind:key="todo.id" v-for='todo in todos'>
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
        </div>
        
    </div>
</template>

<script>
import TodoItem from './TodoItem.vue'

export default {
    name: 'Todos',
    components: {
        TodoItem
    },
    props: ['todos']
}
</script>

<style scoped>

</style>