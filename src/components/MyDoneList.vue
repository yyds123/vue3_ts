<template>
  <div id="done">
    <h1 class="head">
      <span>已经完成</span>
      <span class="count" v-if="donelist.length">{{donelist.length}}</span>
    </h1>
    <ul id="donelist" v-if="donelist">
      <MyItem v-for="item in donelist" :key="item.id" :item="item" :deleteItem="deleteItem" :changeCheck="changeCheck"/>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import MyItem from "@/components/MyItem.vue";
export default defineComponent({
  name: 'MyDoneList',
  components:{MyItem},
  props:['donelist','deleteItem','changeCheck'],
});
</script>

<style scoped lang="less">
#done{
  overflow: hidden;
  ul>li{
    opacity: 0.5;
  }
}
</style>
