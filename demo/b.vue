<template>
    <div>
        <label>限额</label>
        <cube-switch v-model="value">
            Switch
        </cube-switch>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                value: true,
                initUpdateNum: 0
            }
        },
        updated() {
            this.initUpdateNum++
            this.$emit('bComponentChangeEvent', this.initUpdateNum)
            console.log(`b更新次数`, this.initUpdateNum)
        },
    }
</script>

<style scoped>
    /* Switch开关样式 */
    /* 必须是input为 checkbox class 添加 switch 才能实现以下效果 */
    input[type='checkbox'].switch{
        outline: none;
        appearance: none;
        -webkit-appearance: none;
        -moz-appearance: none;
        position: relative;
        width: 40px;
        height: 20px;
        background: #ccc;
        border-radius: 10px;
        transition: border-color .3s, background-color .3s;
    }

    input[type='checkbox'].switch::after {
        content: '';
        display: inline-block;
        width:20px;
        height:20px;
        border-radius: 50%;
        background: #fff;
        box-shadow: 0 0 2px #999;
        transition:.4s;
        top: 2px;
        position: absolute;
        left: 2px;
    }

    input[type='checkbox'].switch:checked {
        background: rgb(19, 206, 102);
    }
    /* 当input[type=checkbox]被选中时：伪元素显示下面样式 位置发生变化 */
    input[type='checkbox'].switch:checked::after {
        content: '';
        position: absolute;
        left: 55%;
        top: 2px;
    }
</style>
