<template>
  <div>
      <form action="" @submit.prevent="addTodo">
          <input type="text" v-model="title" name="title" placeholder="请添加待办事项...">
          <input type="submit" value="添加" class="btn">
      </form>
  </div>
</template>

<script>
// import uuid from "uuid"; 本地测试
export default {
  name: "AddTodo",
  data(){
      return{
          title:''
      }
  },
  methods:{
      addTodo(e){
        //阻止闪动 方式一:  e.preventDefault();  方式二: @click.prevent
        //   console.log(this.title);
        const newTodo = {
            // id: uuid.v4(),
            title: this.title,
            completed: false
        };
        
        // console.log(newTodo);
        //注册事件 父级触发事件 使得子组件添加内容
        this.$emit('handleAdd', newTodo);
        this.title='';
      }
  },
  props: {}
};
</script>
<style scoped lang="scss">
form{
    display: flex;
}
input[type="text"]{
    flex: 10;
    padding: 5px;
}
input[type="submit"]{
    flex: 2;
}
</style>
