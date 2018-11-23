<template>
    <el-form ref="cardForm" :model="form" v-on:submit.native.prevent :rules="rules">
        <el-form-item>
            <el-input v-model="form.number" placeholder="Credit card number"></el-input>
        </el-form-item>
        <el-form-item>
            <el-col :span="12">
                <el-date-picker type="month" format="MM/yy" placeholder="Expiration date"
                                v-model="form.expirationDate"></el-date-picker>
            </el-col>
            <el-col :span="12">
                <el-input v-model="form.cvc" placeholder="Security code"></el-input>
            </el-col>
        </el-form-item>
        <el-form-item>
            <el-input v-model="form.cardHolder" placeholder="Card holder"></el-input>
        </el-form-item>
        <el-form-item>
            <el-col :span="6">
                <el-select v-model="form.documentTye" placeholder="Document type">
                    <el-option
                            v-for="item in form.documentTypes"
                            :key="item.id"
                            :label="item.name"
                            :value="item.name">
                    </el-option>
                </el-select>
            </el-col>
            <el-col :span="12">
                <el-input v-model="form.document" placeholder="Document number"></el-input>
            </el-col>
        </el-form-item>
        <el-form-item>
            <el-button v-on:click="onSubmit" type="primary">Generate token</el-button>
        </el-form-item>
    </el-form>
</template>

<script>

    import axios from 'axios';

    export default {
        name: 'CardForm',
        props: {
            publicToken: {
                required: true
            }
        },
        data() {
            return {
                form: {
                    number: null,
                    cvc: null,
                    expirationDate: null,
                    cardHolder: null,
                    document: null,
                    documentTypes: [],
                    documentTye: null
                },
                rules: {}
            }
        },
        watch: {
            publicToken() {
                this.loadDocumentTypes();
            }
        },
        mounted() {
            this.loadDocumentTypes();
        },
        methods: {
            loadDocumentTypes() {
                axios.get('https://api.mercadopago.com/v1/identification_types', {params: {"public_key": this.publicToken}})
                    .then(response => {
                        this.form.documentTypes = response.data;
                    })
                    .catch(error => {
                        console.log(error);
                    });
            },
            onSubmit() {
                this.$refs['publicKeyForm'].validate((valid) => {
                    if (valid) {
                        console.log("Valid");
                        //this.$emit('cardToken', this.form);
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
