<template>
  <MyHeader :receive="receive"/>
  <div id="todolist_main">
    <MyTodoList :todolist="todolist" :deleteItem="deleteItem" :changeCheck="changeCheck"/>
    <MyDoneList :donelist="donelist" :deleteItem="deleteItem" :changeCheck="changeCheck"/>
  </div>
</template>

<script lang="ts">
import {defineComponent, reactive} from 'vue';
import MyHeader from './components/MyHeader.vue';
import MyTodoList from './components/MyTodoList.vue';
import MyDoneList from './components/MyDoneList.vue';
interface todo{
  id:string,
  title:string,
  done:boolean
}
export default defineComponent({
  name: 'App',
  components: {
    MyHeader,MyTodoList,MyDoneList
  },
  setup(){
    //读取localstorage
    const read = (key:string) => {
      const value = localStorage.getItem(key)
      if (value){
        return JSON.parse(value)
      }
      return []
    }
    //设置localstorage
    const set = (key:string,value:todo[]) => {
      localStorage.setItem(key,JSON.stringify(value))
    }
    let todolist = reactive<todo[]>(read('todolist'))
    let donelist = reactive<todo[]>(read('donelist'))

    //添加todo
    const receive = (x:todo)=>{
      todolist.push(x)
      set('todolist',todolist)
    }
    //删除todo
    const deleteItem = (id:string) => {
      let index:number = todolist.findIndex(item=>{return item.id===id})
      if(index==-1){
        index = donelist.findIndex(item=>{return item.id===id})
        donelist.splice(index,1)
        set('donelist',donelist)
      }
      else {
        todolist.splice(index,1)
        set('todolist',todolist)
      }
    }
    //更改选中状态
    const changeCheck = (id:string) => {
      let index:number = todolist.findIndex(item=>{return item.id===id})
      let item:todo
      if(index==-1){
        index = donelist.findIndex(item=>{return item.id===id})
        item = donelist[index]
        item.done = !item.done
        donelist.splice(index,1)
        todolist.push(item)
      }
      else {
        item = todolist[index]
        todolist.splice(index,1)
        item.done = !item.done
        donelist.push(item)
      }
      set('todolist',todolist)
      set('donelist',donelist)
    }
    return {
      receive,
      todolist,
      deleteItem,
      donelist,
      changeCheck
    }
  }
});
</script>

<style lang="less">
#app {
  width: 1000px;
  margin: 100px auto;
}
ul{
  list-style: none;
  margin: 0;
  padding: 0;
}
#todolist_main{
  background-color: rgb(205,205,205);
  padding: 0 50px;
  overflow: hidden;
}
.head{
  margin: 20px 0;
  position: relative;
}
.count{
  float: right;
  display: inline-block;
  height: 25px;
  width: 25px;
  background-color: rgb(230,230,250);
  font-size: 20px;
  line-height: 25px;
  text-align: center;
  border-radius: 50%;
  position: absolute;
  margin-right: 20px;
  top: 50%;
  right: 0;
  transform: translateY(-50%);
}
li{
  border-left: 5px solid rgb(98,154,156);
  margin-bottom: 15px;
  height: 40px;
  line-height: 40px;
  font-size: 25px;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: space-between;
  .checkbox{
    height: 30px;
    width: 30px;
    margin-left: 10px;
    cursor: pointer;
  }
  .text{
    margin: 0 10px;
    text-align: left;
    flex: 1;
  }
  .delete{
    margin-right: 20px;
    height: 30px;
    width: 30px;
    box-sizing: border-box;
    border: 2px solid rgb(204,204,204);
    cursor: pointer;
    border-radius: 50%;
    position: relative;
    div{
      position: relative;
      width: 20px;
      height: 20px;
      border-radius: 50%;
      top: 50%;
      left: 50%;
      transform: translate(-50%,-50%);
      background-color: rgb(204,204,204);
    }
  }
}
</style>
