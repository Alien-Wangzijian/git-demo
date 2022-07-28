<template>
  <div class="list-footer">
    <li v-if="list.length != 0">
      <b>
        <input type="checkbox" 
        :checked='allDone'
        @change="allChange">
        已完成: {{isDone}} / 全部: {{list.length}}
      </b>
      <b @click="clear">清空已完成任务</b>
    </li>
    <li v-else>
      暂无数据
    </li>
  </div>
</template>

<script>
export default {
  props: ["list", 'isDone', 'allDone'],
  data() {
    return {};
  },
  methods: {
    // 点击全选 单选同步
    allChange(e){
      this.$emit('allChange', e.target.checked)
    },
    // 清空已完成
    clear() {
      this.$emit('clear')
    },
  },
};
</script>