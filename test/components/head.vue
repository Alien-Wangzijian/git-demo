<template>
    <div>
    <div class="head">
        <h2>拾忆记事本</h2>
        <p>记录生活点点滴滴，写下生活每一个美好</p>
        <div class="input">
            <span>内容</span><input type="text"  @keyup.enter="add" v-model="title"  placeholder="请输入你要记事的内容"/><span @click="add">确认</span>
        </div>
    </div>
        
    </div>
</template>
<script>
import { nanoid } from 'nanoid';

export default {
    name: 'Head',
    data() {
        return {
            title:'',
        }
    },
    methods: {
        add(){
        //输入不为空
            if(this.title.length != 0){
                let obj = { id: nanoid(), title: this.title, done: false}
                this.$emit('addTitle', obj)
            }else{
                alert('输入内容不能为空')
            }
            this.title = ''
            },
        },
}
</script>