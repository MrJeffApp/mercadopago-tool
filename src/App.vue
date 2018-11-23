<template>
    <el-container>
        <el-header>
            <el-row type="flex" justify="center">
                <el-col :span="12">
                    <h1>MercadoPago card token generator</h1>
                </el-col>
            </el-row>
        </el-header>
        <el-main>
            <el-row type="flex" justify="center">
                <el-col :span="6">
                    <PublicKeyForm v-on:publicKey="onToken"/>
                    <CardForm v-if="showCardForm" :publicToken="publicToken"/>
                </el-col>
            </el-row>
        </el-main>
    </el-container>
</template>

<script>
    import stringUtils from 'voca';
    import PublicKeyForm from './components/PublicKeyForm.vue'
    import CardForm from './components/CardForm.vue'

    export default {
        name: 'app',
        components: {
            PublicKeyForm,
            CardForm
        },
        data() {
            return {
                publicToken: null
            };
        },
        computed: {
            showCardForm() {
                return !stringUtils.isBlank(this.publicToken);
            }
        },
        methods: {
            onToken(token) {
                this.publicToken = token;
            }
        }
    }
</script>

<style>

</style>
