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
                    <PublicKeyForm v-show="showTokenForm" v-on:publicKey="onToken"/>
                    <CardForm v-show="showCardForm"/>
                </el-col>
            </el-row>
        </el-main>
    </el-container>
</template>

<script>
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
                showTokenForm: true,
                publicToken: null,
                showCardForm: true,
            };
        },
        methods: {
            onToken(token) {
                this.publicToken = token;
                this.showTokenForm = false;
                this.showCardForm = true;
            }
        }
    }
</script>

<style>

</style>
