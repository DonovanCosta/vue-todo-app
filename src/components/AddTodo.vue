<template>
    <div>
        <form @submit="addTodo" class="justify-content-center">
            <div class="form-group">
                <div class="input-group mt-5">
                    <input type="text" name="title" placeholder="Add Todo..." v-model="title">
                    <div class="input-group-append">
                         <button class="btn btn-primary" type="submit" value="submit" >Add Task</button>
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>

<script>
import {v4 as uuid} from 'uuid';

export default {

    name: "AddTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e){
            e.preventDefault();
            const newTodo = {
                id: uuid(),
                title: this.title,
                completed: false
            }

            // send to the parent
            this.$emit('add-todo', newTodo)

            this.title='';
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
        padding: 5px;
    }
</style>