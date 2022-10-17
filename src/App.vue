<template>
  <div id = "App">
  <h1>Todo App</h1><h3>with Vue.js</h3>
  <Addform
    @add-task="AddTask"
  />
  <hr>
  <TodoList
  v-bind:todos="todos"
  @remove-task="RemoveTask"
  @finish-edit-task="EditTask"
  @done-task="DoneTaskSave"
  />
  <button class="del-done" v-on:click="DeleteDone">Удалить выполненные задачи</button>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import Addform from '@/components/Addform'
export default {
  name: 'App',
  data() {
    return {
      todos: []
    }
  },
  components: {
    TodoList,
    Addform
  },
  methods: {
    RemoveTask(id){
      this.todos = this.todos.filter((task) => task.id !== id);
      this.setToLocal();
    },
    DeleteDone(){
      this.todos = this.todos.filter((task) => task.completed == false);
      this.setToLocal();
    },
    AddTask(todo){
      this.todos.push(todo)
      this.setToLocal();
    },
    EditTask(id, newtext){
    const index = this.todos.findIndex((task) => task.id === id)
    console.log(index)
    const newtask = {
        id: id,
        text: newtext,
        completed: false
      }
      this.todos.splice(index, 1, newtask);
    },
    setToLocal(){
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    DoneTaskSave(id){
      this.setToLocal();
    }
    
  },
  mounted(){
    if(localStorage.todos){
      this.todos = JSON.parse(localStorage.getItem('todos'));
    }
  }
}

</script>

<style>
html{
  background-image: url(./assets/backgrnd1.png);
  background-repeat: no-repeat;
  background-size: cover;
  background-attachment: fixed;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  justify-content: center;
  align-content: center;
}
h1, h3{
  text-align: center;
  width: 60%;
}
.del-done{
  padding: 5pt;
  margin-top: 3rem;
  background-color: rgb(76, 99, 72);
  border: 1px solid black;
  color: #e0e7e1;
  font-size: medium;
}

</style>
