<template>
     <div class="card mb-3">
        <div class="card-body todo-item">
            <p class="card-text mb-1" v-bind:class="{'is-complete':todo.completed}">
                <input type="checkbox" v-on:change="markComplete">
                {{todo.title}}
                <!-- emit a click event that we acces in the app.vue  -->
            </p>
            <button @click="$emit('del-todo', todo.id)" class="btn btn-danger delete_btn">Delete Task</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    methods: {
        markComplete(){
           this.todo.completed = !this.todo.completed;
        }
    }

}
</script>

<style scoped>

    .todo-item {
        background: #f4f4f4;
        border-bottom: 1px #ccc dotted;
    }

    .is-complete {
        text-decoration: line-through;
    }
    .delete_btn {
        position: relative;
        top: 0;
        bottom: 0;
        right: 10px;
        height: 35px;
        margin: auto;
    }
</style>