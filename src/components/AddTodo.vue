<template>
    <div>
        <form @submit="addTodo"> <!-- On submit, traverse up to the array in App.vue -->
            <input type="text" v-model="title" name="title" placeholder="Add Todo...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
//import uuid from 'uuid';
export default {
    name: "AddTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                //id: uuid.v4(), // don't need this, since we have JSON placeholders give us an id already; previously used this to randomize ids
                title: this.title,
                completed: false
            }
            // Send up to parent
            this.$emit('add-todo', newTodo);
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding:5 px;
    }

    input[type="submit"] {
        flex:2;
    }
</style>
