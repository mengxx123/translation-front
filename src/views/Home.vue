<template>
    <my-page title="翻译">
        <ui-text-field v-model="input" multiLine :rors="6" />
        <div class="operation">
            <ui-raised-button class="btn" label="翻译" primary hintText="仅支持英译汉" @click="translate" />
        </div>
        <div v-if="result">
            {{ result.translation[0] }}
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
                result: null
            }
        },
        mounted() {
        },
        methods: {
            translate() {
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
