<template>
  <div class="todo-item" :class="{'is-complete' : todo.completed}">
    <p>
      <input type="checkbox" @change="makrComplete">
      {{todo.title}}
      <button class="del" @click="$emit('deleteItem',todo.id)">X</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    makrComplete(){
      // console.log(this.todo);
      this.todo.completed = !this.todo.completed;
    }
  }
  // props: {
  //     todos: {
  //         type: Array
  //     }
  // }
};
</script>

<style scoped>
.todo-item {
  background: #fefefe;
  padding: 10px;
  border-bottom: 1px dotted #ccc;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 8px;
  /* padding: 6px; */
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>

