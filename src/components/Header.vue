<template>
  <div class="head">
    <h2>ToDo ~</h2>
    <p>记录生活点点滴滴，写下生活每一个美好</p>
    <div class="input">
      <input type="text" v-model.trim="title" @keyup.enter="add" placeholder="请输入你要记事的内容" />
      <span @click="add">添加</span>
    </div>
  </div>
</template>

<script>
// npm i nanoid
import { nanoid } from "nanoid";
export default {
  name: "Header",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    // 输入添加
    add() {
      // 输入不为空
      if(this.title.length !== 0){
        // 拼接对象
        let obj = {id: nanoid(), title: this.title, done: false}
        // 子传父
        this.$emit('addTitle', obj)
      }
      // 清空输入框
      this.title = ''
    },
  },
};
</script>

