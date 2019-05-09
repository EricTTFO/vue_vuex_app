<template>
  <div class>
    <div v-for="(todo,subscriptValue) in todos" :key="subscriptValue">
        <!-- <TodoItem :todo='todo' @deleteItem='ice'/> -->
        <TodoItem :todo='todo' @deleteItem="$emit('handleDelete', todo.id)"/>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  name: "Todos",
  //   props: ["todos"]
  props: {
    todos: {
      type: Array
    }
  },
  components: {
      TodoItem
  },
//   methods: {
//       ice(id){
//           console.log(id);
//       }
//   }
};
</script>

<style scoped>
</style>

