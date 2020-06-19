<template>
    <div>
        <label>姓名</label>
        <input v-model="name"/>
        <input v-model="address"/>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                name: '张三',
                address: "广东-深圳",
                initUpdateNum: 0,
                hasData: true,
                initialDataConfiguration: null
            }
        },
        updated() {
            this.initUpdateNum = this.initUpdateNum + 1
            this.$emit('aComponentChangeEvent', this.initUpdateNum)
            console.log(`a更新次数`, this.initUpdateNum)
        },
        methods: {
            resetData() {
                Object.assign(this.$data, this.$options.data.apply(this));
                this.initUpdateNum = -1
            },
        }
    }
</script>

<style scoped>
input {
    height: 50px;
    width: 100%;
    font-size: 20px;
    border: 1px solid #ccc;
}
</style>
