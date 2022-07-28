<template>
    <div>
        <ul class="list list1">
        <!-- v-for循环列出列表 -->
        <li v-for="(item,index) in list" :key='index+1'>
        <!-- 前面的序号 -->
        <span class="xh">{{index+1}}</span>
        <!-- 列表内容 -->
        <span>{{item.title}}</span>
        <!-- 关闭按钮 -->
        <!-- 添加点击移除事件，要传形参 -->
        <span class="qc" @click="remove()"></span>
        </li>
    </ul>
    </div>
</template>
<script>
export default {
    name: 'Content',
    props: ['list']
}
</script>