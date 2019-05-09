<template>
  <div id="app">
    <!-- {{ msg }}  {{ todos[0].id }} -->
    <!-- <div class="" v-for="todo in todos" :key="todo.id"> -->
      <!-- {{ todo.title }} -->
    <!-- </div> -->
    <!-- 也可使用下标值 -->

  <Todos :todos='todos' @handleDelete='handleDelete'/>  
  </div>
</template>

<script>
import Todos from './components/Todos'
export default {
    name: 'app',
    //返回数据
    data(){
      return{
        msg: 'helle',
        todos: [
          {
            id: 1,
            title: '代办事项1',
            completed: false
          },
          {
            id: 2,
            title: '待办事项2',
            completed: false
          },
          {
            id: 3,
            title: '待办事项3',
            completed: false
          }
        ]
      }
    },
    components: {
      Todos
    },
    methods: {
      handleDelete(id){
        // console.log(id);
        this.todos = this.todos.filter(todo => todo.id !== id);
      }
    }
}
</script>


<style lang="scss">

  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body{
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

</style>
