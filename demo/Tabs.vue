<template>
    <div>
        <app-header :backFn="backFn" title="测试用户是否操作了数据"></app-header>
        <div class="tabs">
            <ul>
                <li @click="chooseItem(index)" v-for="(item, index) in list" :key="item.index">{{item}}</li>
            </ul>
        </div>
        <div class="content">
            <a-component ref="resetAComponentData" reset-Data="resetFlag" @aComponentChangeEvent="aComponentChangeEvent" v-show="currentIndex === 0"/>
            <b-component reset-Data="resetFlag" @bComponentChangeEvent="aComponentChangeEvent" v-show="currentIndex === 1"/>
            <c-component reset-Data="resetFlag" @cComponentChangeEvent="aComponentChangeEvent" v-show="currentIndex === 2"/>
        </div>

    </div>
</template>

<script>
    import a from './a.vue'
    import b from './b.vue'
    import c from './c.vue'

    export default {
        components: {
            aComponent: a,
            bComponent: b,
            cComponent: c
        },
        data() {
            return {
                currentIndex: 0,
                list: ['a', 'b', 'c'],
                initUpdateNum: 0,
            }
        },
        methods: {
            aComponentChangeEvent(data) {
                this.initUpdateNum = data
            },
            showBtn() {
                this.$createDialog({
                    type: 'confirm',
                    title: '我是标题',
                    content: '我是内容',
                    confirmBtn: {
                        text: '确定按钮',
                        active: true,
                        disabled: false,
                        href: 'javascript:;'
                    },
                    cancelBtn: {
                        text: '取消按钮',
                        active: false,
                        disabled: false,
                        href: 'javascript:;'
                    },
                    onConfirm: () => {
                        this.next()
                    },
                    onCancel: () => {
                        this.initUpdateNum = 0
                        this.$refs.resetAComponentData.resetData()

                    }
                }).show()
            },

            chooseItem(index) {
                if (index === this.currentIndex) {
                    return ;
                }
                if(this.initUpdateNum > 0) {
                    return new Promise((resolve) => {
                        this.showBtn()
                    }).then(() => {
                        resolve()
                        this.currentIndex = index
                    })
                } else {
                    this.currentIndex = index
                }
            },

            async next() {
                await this.submitForm()
                await this.successTips()
            },

            submitForm() {
                console.log('submit!!!')
            },
            successTips() {
                this.initUpdateNum = 0
                this.$toast('success')
            },
            backFn() {
               if (this.initUpdateNum > 0) {
                   this.showBtn()
               }
            },
        }
    }
</script>

<style scoped>
    ul {
        height: 50px;
        display: flex;
    }
    li {
        font-size: 40px;
        height: 100%;
        border: 1px solid #ccc;
        flex: 1;
        text-align: center;
    }
</style>
