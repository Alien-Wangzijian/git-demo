<template>
    <div>
        <ul class="list2 list">
        <li v-if="list.length!=0">
        <b>
            总数：{{list.length}}
        </b>
        <b @click="clear">清除</b>
        </li>
        <li v-else>
        暂无数据
        </li>
    </ul>
    </div>
</template>
<script>
export default {
    name: 'Footer',
    props: ['list','clear']
}
</script>