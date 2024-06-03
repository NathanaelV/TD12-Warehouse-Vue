<template>
    <div>
        <h1>Cadastrar Galpão</h1>
        <div>

            <v-alert v-if="msg != null" type="info">
                {{ msg }}
                <ul v-for="error_msg in error_messages">
                    <li>{{ error_msg }}</li>
                </ul>
            </v-alert>

            <v-form v-on:submit.prevent>
                <v-text-field label="Nome" v-model="form.name" placeholder="Nome do galpão"></v-text-field>
                <v-text-field label="Código" v-model="form.code" placeholder="Código do galpão"></v-text-field>
                <v-text-field label="Endereço" v-model="form.address" placeholder="Endereço do galpão"></v-text-field>
                <v-text-field label="Cidade" v-model="form.city" placeholder="Cidade"></v-text-field>
                <v-text-field label="CEP" v-model="form.cep" placeholder="CEP"></v-text-field>
                <v-text-field label="Área" v-model="form.area" placeholder="Área em m²"></v-text-field>
                <v-textarea label="Descrição" v-model="form.description"></v-textarea>

                <v-btn color="primary" v-on:click="postWarehouse">Cadastrar Galpão</v-btn>
            </v-form>
        </div>
    </div>
</template>

<script>
export default {
    name: 'WarehouseNew',

    data() {
        return {
            msg:null,
            form: {
                name:        null,
                code:        null,
                address:     null,
                city:        null,
                cep:         null,
                area:        null,
                description: null,
            },
            error_messages: []
        }
    },

    methods: {
        async postWarehouse() {
            try {

                await this.$http.post('http://localhost:3000/api/v1/warehouses', {

                name: this.form.name,
                code: this.form.code,
                city: this.form.city,
                address: this.form.address,
                cep: this.form.cep,
                area: this.form.area,
                description: this.form.description

                })

                this.msg = 'Galpão Cadastrado com sucesso!'

            } catch(error) {

                this.msg = 'ERRO ao cadastrar o galpão!';
                this.error_messages = error.body.errors;

                // console.log(error);

            }
        }
    }
}
</script>

<style>
.form {
    margin-bottom: 10px;
}

.form input {
    margin: 5px;
}
</style>