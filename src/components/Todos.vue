<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <!-- <h3>{{ todo.title }}</h3> --> <!-- Looping through the todos prop -->
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
    name: "Todos",
    components: {
        TodoItem
    },
    props: ["todos"]
}
</script>

<style scoped>

</style>
