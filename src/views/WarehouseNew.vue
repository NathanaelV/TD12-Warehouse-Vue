<template>
    <div>
        <h1>Cadastrar Galpão</h1>
        <div>

            <div>
                {{ msg }}
                <ul v-for="error_msg in error_messages">
                    <li>{{ error_msg }}</li>
                </ul>
            </div>

            <form v-on:submit.prevent>
                <div class="form">
                    <label>Nome: </label>
                    <input type="text" v-model="form.name" placeholder="Nome do galpão">
                </div>

                <div class="form">
                    <label>Código: </label>
                    <input type="text" v-model="form.code" placeholder="Código do galpão">
                </div>

                <div class="form">
                    <label>Endereço: </label>
                    <input type="text" v-model="form.address" placeholder="Endereço do galpão">
                </div>

                <div class="form">
                    <label>Cidade: </label>
                    <input type="text" v-model="form.city" placeholder="Cidade">
                </div>

                <div class="form">
                    <label>CEP: </label>
                    <input type="text" v-model="form.cep" placeholder="CEP">
                </div>

                <div class="form">
                    <label>Área: </label>
                    <input type="number" v-model="form.area">
                </div>

                <div class="form">
                    <label>Descrição: </label>
                    <textarea v-model="form.description"></textarea>
                </div>

                <div class="form">
                    <button v-on:click="postWarehouse">Cadastrar Galpão</button>
                </div>
            </form>
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