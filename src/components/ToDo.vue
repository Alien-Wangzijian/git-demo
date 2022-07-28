<template>
  <div>
    <ul class="list">
      <!-- v-for循环列出列表 -->
      <li v-for="(item, index) in list" :key='index'>
        <Item 
        :item='item' 
        :index='index' 
        ></Item>
      </li>
    </ul>
  </div>
</template>

<script>
import Item from "../components/Item.vue";
export default {
  name: "ToDo",
  components: {
    Item,
  },
  props: ["list"],
  data() {
    return {};
  },
  methods: {
    // 删除
    // removeByIndex(index) {
    //   this.$emit('removeByIndex', index)
    // },
    clear() {},
  },
};
</script>

<style>
#app .list li #edit {
  display: block;
  width: 34px;
  height: 20px;
  color: #fff;
  background-color: skyblue;
  border-radius: 5px;
  cursor: pointer;
  float: right;
}
#app .list li #edit:hover {
  color: black;
  background-color: orange;
}
.ch {
  margin-right: 10px;
  vertical-align: middle;
}
</style>