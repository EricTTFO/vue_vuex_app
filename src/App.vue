<template>
  <div id="app">
    <!-- {{ msg }}  {{ todos[0].id }} -->
    <!-- <div class="" v-for="todo in todos" :key="todo.id"> -->
    <!-- {{ todo.title }} -->
    <!-- </div> -->
    <!-- 也可使用下标值 -->
    <Header/>
    <AddTodo v-on:handleAdd="handleAdd"/>
    <Todos :todos="todos" @handleDelete="handleDelete"/>
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import AddTodo from "./components/AddTodo";
import Todos from "./components/Todos";
import axios from "axios";
export default {
  name: "app",
  //返回数据
  data() {
    return {
      msg: "hello",
      todos: []
    };
  },
  components: {
    Todos,
    Header,
    AddTodo
  },
  methods: {
    handleDelete(id) {
      // console.log(id);
      axios.delete("https://jsonplaceholder.typicode.com/todos/${id}")
      .then(res => (this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err))
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
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 15px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
