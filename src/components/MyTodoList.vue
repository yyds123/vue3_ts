<template>
  <div id="todo">
    <h1 class="head">
      <span>正在进行</span>
      <span class="count" v-if="todolist.length">{{todolist.length}}</span>
    </h1>
    <ul id="todolist" v-if="todolist">
      <MyItem v-for="item in todolist" :key="item.id" :item="item" :deleteItem="deleteItem" :changeCheck="changeCheck"/>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import MyItem from "@/components/MyItem.vue";

export default defineComponent({
  name: 'MyTodoList',
  components:{MyItem},
  props:['todolist','deleteItem','changeCheck'],
});
</script>

<style scoped lang="less">
#todo{
  overflow: hidden;
}
</style>
