<template>
    <div id="app">
        <div class="container">
            <div class="row align-items-center">
                <div class="col-12 justify-content-center">
                    <AddTodo v-on:add-todo="addTodo"/>
                </div>
            </div>
            <div class="row justify-content-center">
                <div class="col-sm-8">
                    
                    <!-- v-bind is a template directives in this case bind the todos from data to the todos in v-bind -->
                    <!--  Dynamically bind one or more attributes, or a component prop to an expression.
                            When used to bind the class or style attribute, it supports additional value types such as Array or Objects.
                            See linked guide section below for more details.
                            When used for prop binding, the prop must be properly declared in the child component. -->

                    <!-- catching event emitted using the v-on:<event name > -->
                    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';

import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  // data() is a function where we will store the todo data.
  data(){
      return {
         todos: [
             {
                id:1,
                title: "Todo One",
                completed: false
             },
             {
                id:2,
                title: "Todo Two",
                completed: true
             },
             {
                id:3,
                title: "Todo Three",
                completed: false
             }

         ]
      }
  },
  methods: {
      deleteTodo(id){ 
          console.log(id)
            axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                .then(this.todos = this.todos.filter(todo => todo.id !== id))
                .catch(err => console.log(err))

        //   this.todos = this.todos.filter(todo => todo.id !== id)
      },
      addTodo(newTodo){
            const { id, title, completed} = newTodo

            console.log(newTodo)

            axios.post('https://jsonplaceholder.typicode.com/todos',{
                id,
                title,
                completed
            })
            
            .then(res => this.todos = [...this.todos, res.data] )
            .catch(err => console.log(err))
        //   this.todos = [...this.todos, newTodo];
      }
  },
  // lifecycle hook 
  created(){
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err))

  }
}
</script>

<style>
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    body {
        font-family: Arial, Helvetica, sans-serif;
        line-height: 1.4;
    }

    /* .btn{
        display: inline-block;
        border: none;
        background: #555;
        color: #fff;
        padding: 7px 20px;
        cursor: pointer;
    }
    .btn:hover {
        background: #666;
    } */
</style>
