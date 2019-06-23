<template>
    <my-page title="翻译" :page="page">
        <div class="common-container container">
            <ui-text-field v-model="input" multiLine :rors="6" label="英文" />
            <div class="operation">
                <ui-raised-button class="btn" label="翻译" primary hintText="仅支持英译汉" @click="translate" />
            </div>
            <div v-if="result">
                {{ result.translation[0] }}
            </div>
        </div>
    </my-page>
</template>

<script>
    export default {
        data () {
            return {
                input: '',
//                input: '翻译',
//                input: 'translate',
                result: null,
                page: {
                    menu: [
                        // {
                        //     type: 'icon',
                        //     icon: 'search',
                        //     href: 'https://search.yunser.com?utm_source=calculator',
                        //     target: '_blank',
                        //     title: '搜索'
                        // },
                        {
                            type: 'icon',
                            icon: 'apps',
                            href: 'https://app.yunser.com?utm_source=translation',
                            target: '_blank',
                            title: '应用'
                        }
                    ]
                }
            }
        },
        mounted() {
        },
        methods: {
            translate() {
                if (!this.input) {
                    this.$message({
                        type: 'danger',
                        text: '请输入英文'
                    })
                    return
                }
                this.$http.get(`/translate?q=${this.input}`).then(
                    response => {
                        let data = response.data
                        console.log(data)
                        this.result = data
                    },
                    response => {
                        console.log(response)
                    })
            }
        }
    }
</script>

<style lang="scss" scoped>
    .operation {
        margin-bottom: 16px;
        /*margin-top: 16px;*/
    }
</style>
