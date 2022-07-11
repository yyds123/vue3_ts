<template>
  <div id="topbar">
    <span>Todolist</span>
    <input type="text" placeholder="todo" @keyup.enter = "addTodo">
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import {nanoid} from "nanoid";

interface todo{
  id:string,
  title:string,
  done:boolean
}
export default defineComponent({
  name: 'MyHeader',
  props:['receive'],
  setup(props){
    let todo:todo
    const addTodo = (e:any)=>{
      todo = {id:nanoid(),title:e.target.value,done:false}
      props.receive(todo)
      e.target.value = ''
    }
    return {
      addTodo
    }
  }
});
</script>

<style scoped lang="less">
  #topbar {
    background-color: rgb(50, 50, 50);
    padding: 0 50px;
    height: 60px;
    color: white;
    font-size: 30px;
    line-height: 60px;
    position: relative;
    input {
      display: inline-block;
      float: right;
      width: 500px;
      height: 20px;
      font-size: 20px;
      position: relative;
      top: 50%;
      transform: translateY(-50%);
    }
  }
</style>
