<template>
    <el-form ref="publicKeyForm" :model="form" v-on:submit.native.prevent :rules="rules" :inline="true">
        <el-form-item prop="publicKey" label="MercadoPago Public Key:">
            <el-input v-model="form.publicKey" placeholder="Paste public key here"></el-input>
        </el-form-item>
        <el-form-item>
            <el-button v-on:click="onSubmit" type="primary">Show card form</el-button>
        </el-form-item>
    </el-form>
</template>

<script>
    export default {
        name: 'PublicKeyForm',
        data() {
            return {
                form: {
                    publicKey: null
                },
                rules: {
                    publicKey: [
                        { required: true, message: 'Please insert your public key', trigger: 'blur'},
                        { len: 41, message: 'Length should be 41 characters', trigger: 'blur'}
                    ]
                }
            }
        },
        methods: {
            onSubmit() {
                this.$refs['publicKeyForm'].validate((valid) => {
                    if (valid) {
                        this.$emit('publicKey', this.form.publicKey);
                        return true;
                    } else {
                        return false;
                    }
                });
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
