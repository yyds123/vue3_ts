<template>
  <li v-show="title">
    <input type="checkbox" class="checkbox" :checked="done" @click="changeChecked(id)">
    <span class="text">{{title}}</span>
    <div class="delete" @click="del(id)">
      <div></div>
    </div>
  </li>
</template>

<script lang="ts">
import {defineComponent,ref} from 'vue';

export default defineComponent({
  name: 'MyItem',
  props:['item','deleteItem','changeCheck'],
  setup(props){
    let title = props.item?ref(props.item.title):undefined
    let done = props.item?ref(props.item.done):undefined
    let id = props.item?ref(props.item.id):undefined
    const del = (id:string) => {
        props.deleteItem(id)
    }
    const changeChecked = (id:string) => {
      props.changeCheck(id)
    }
    return {
      title,done,id,del,changeChecked
    }
  }
});
</script>

