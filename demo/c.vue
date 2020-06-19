<template>
    <div>
        <textarea v-model="detail"/>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                detail: '',
                initUpdateNum: 0,
            }
        },
        updated() {
            this.initUpdateNum++
            this.$emit('cComponentChangeEvent', this.initUpdateNum)
            console.log(`c更新次数`, this.initUpdateNum)
        },
    }
</script>

<style scoped>

</style>
