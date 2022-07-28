<template>
  <div id="app">
    <Head @addTitle = 'addTitle'></Head>
    <Content :list = 'list'></Content>
    <Footer :list = 'list' :clear = 'clear'></Footer>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Head from './components/head.vue';
import Content from './components/content.vue';
import Footer from './components/footer.vue';

export default {
  name: 'App',
  components: {
    Head,
    Content,
    Footer
  },
  methods: {
    clear(){
      
    },
    addTitle(title){
      console.log(title.id)
      this.list.push(title)
    }
  },
  data() {
    return {
      list:[
        {id: '1', title: '学习', done: true},
        {id: '2', title: '吃饭 ', done: false},
        {id: '3', title: '睡觉', done: true}
      ],
      title: "",
    }
  },
}
</script>

<style lang="sass">
  
</style>
