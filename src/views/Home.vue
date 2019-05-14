<template>
  <div id="app">
    <!-- {{ msg }}  {{ todos[0].id }} -->
    <!-- <div class="" v-for="todo in todos" :key="todo.id"> -->
    <!-- {{ todo.title }} -->
    <!-- </div> -->
    <!-- 也可使用下标值 -->
    
    <AddTodo v-on:handleAdd="handleAdd"/>
    <Todos :todos="todos" @handleDelete="handleDelete"/>
  </div>
</template>

<script>

import AddTodo from "../components/AddTodo";
import Todos from "../components/Todos";
import axios from "axios";
export default {
  name: "Home",
  //返回数据
  data() {
    return {
      msg: "hello",
      todos: []
    };
  },
  components: {
    Todos,
    AddTodo
  },
  methods: {
    handleDelete(id) {
      console.log(id);
      axios.delete("https://jsonplaceholder.typicode.com/todos/${id}")
      
      .then(res => (this.todos = this.todos.filter(todo => todo.id !== id))
      // .catch(err => console.log(err))
      // this.todos = this.todos.filter(todo => todo.id !== id
      )},
    handleAdd(newTodo) {
      // console.log(newTodo);
      // this.todos.unshift(newTodo);
      //主流 方式:
      //解构形式编写
      const { title, completed } = newTodo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(res => (this.todos = [res.data, ...this.todos]))
        .catch(err => console.log(err));
      //相当于 const title = newTodo.title;const completed = newTodo.completed;
    }
  },
  created() {
    //数据请求
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => {
        console.log(res.data)
        this.todos = res.data;
      })
      .catch(err => console.log(err));
  }
};
</script>


<style lang="scss">

</style>
