<template>
  <div id="app">
    <Header @addTitle='add'></Header>
    <!-- 通过子传父 -->
    <!-- <ToDo :list='list' @removeByIndex='removeByIndex'></ToDo> -->

    <ToDo :list='list'></ToDo>
    <Footer 
    :list="list" 
    :isDone='isDone' 
    :allDone='allDone' 
    @allChange='allChange' 
    @clear='clear'
    ></Footer>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import ToDo from "./components/ToDo.vue";
import Footer from "./components/Footer.vue";

// 导入bus
import bus from "./eventBus";
export default {
  name: "App",
  components: { Header, ToDo, Footer },
  data() {
    return {
      list: [
        { id: "1", title: "学习", done: true },
        { id: "2", title: "听歌", done: false },
        { id: "3", title: "运动", done: true },
      ],
    };
  },
  methods: {
    // 添加
    add(title) {
      this.list.unshift(title);
    },
    // 点击全选 单选同步
    allChange(done) {
      this.list.forEach((item) => {
        item.done = done;
      });
    },
    // 删除已完成
    clear() {
      this.list.forEach((item, index) => {
        // 如果选中
        if (item.done) {
          // 删除
          this.list.splice(index, 1);
        }
      });
    },
  },
  computed: {
    // 已完成的个数
    isDone() {
      return this.list.filter((item) => item.done).length;
    },
    // 全选的状态 => 取决于每个单选框的状态
    allDone() {
      return this.list.every((item) => item.done);
    },
  },
  created() {
    // 通过下标删除
    bus.$on("removeByIndex", (index) => {
      this.list.splice(index, 1);
    });
    // 改变单选框的状态
    bus.$on("stateChange", (obj) => {
      this.list.some((item) => {
        if (item.id == obj.id) {
          item.done = obj.done;
          return true;
        }
      });
    });
    bus.$on('titleChange', (obj) =>{
      this.list.some((item) => {
        if(item.id == obj.id){
          item.title = obj.title;
          return true;
        }
      })
    })
  },
};
</script>

