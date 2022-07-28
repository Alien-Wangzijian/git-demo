<template>
  <div>
    <input type="checkbox" class="ch" 
    :checked='item.done'
    @change="stateChange">
    <!-- 前面的序号 -->
    <span class="xh">{{index+1}}</span>
    <!-- 列表内容 -->
    <span v-show = "!item.isEdit">{{item.title}}</span>
    <input type="text" 
    v-show = "item.isEdit" 
    :value = 'item.title'
    @blur = 'hanlerBlur(item, $event)'
    ref = 'inputTitle'
    >
    <!-- 编辑 -->
    <span id="edit" @click= 'edit(item)'>编辑</span>
    <!-- 添加点击移除事件，要传形参 -->
    <span class="qc" @click="remove(index)"></span>
  </div>
</template>

<script>
// 导入eventBus
import bus from '../eventBus'
export default {
  props: ["item", "index"],
  methods: {
    remove(index) {
      // this.$emit('removeByIndex', index)
      bus.$emit('removeByIndex', index)
    },
    stateChange(e){
      bus.$emit('stateChange', {id: this.item.id, done: e.target.checked})
    },
    edit(item){
      // isEdit不是在data中定义的数据 而是后续新增的属性
      // 而后续新增的属性无法被响应式处理 所以视图没有更新(input框没有出来)
      // 解决方案 is.$set(obj, key, value)
      // this.$set 内部会调用一个defineReactive()帮我们对新增属性进行响应式处理 加上set、get 底层调用的事Object.defineProperty(obj, key, value)
      if(item.hasOwnProperty('isEdit')){
        item.isEdit = true
      }else{
        this.$set(item, 'isEdit', true)
      }
      this.$set(item, 'isEdit' ,true);  
      // item.isEdit = true;
      // console.log(item)
      this.$nextTick(() =>{
      this.$refs.inputTitle.focus();
      });
    },
    hanlerBlur(item, e){
      //更新isEdit => 隐藏input框
      item.isEdit = false
      bus.$emit('titleChange', {id: this.item.id, title: e.target.value})
    },
  }
};
</script>

<style >
#app .list li .xh {
  float: left;
  display: block;
  width: 30px;
  border-right: 1px dashed #ccc;
  margin-right: 10px;
}
</style>