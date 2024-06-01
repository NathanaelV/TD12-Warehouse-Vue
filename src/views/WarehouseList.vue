<template>
    <div>
        <h1>Galpões Cadastrados</h1>

        <!-- Exibir os dados no formato de tabela -->
        <!-- <table border="1px">
            <thead>
                <th>Código</th>
                <th>Nome</th>
                <th>Sigla</th>
            </thead>

            <tbody>
                <tr v-for="w in warehouses" :key="w.code">
                    <td>{{ w.id }}</td>
                    <td>{{ w.name }}</td>
                    <td>{{ w.code}}</td>
                </tr>
            </tbody>
        </table> -->

        <!-- Exibir os dados no formato de Card -->
        <div v-for="w in warehouses" :key="w.id">
            <Warehouse
                :name       = "w.name"
                :code       = "w.code"
                :address    = "w.address"
                :city       = "w.city"
                :area       = "w.area"
            />
        </div>
    </div>
</template>

<script>
// Importa componente Warehouse
import Warehouse from '../components/Warehouse.vue'

export default {
    name: 'WarehouseList',

    components: {
        Warehouse
    },

    data() {
        return {
            warehouses: []
        }
    },

    async mounted() {
        this.getWarehouses();
    },

    methods: {
        async getWarehouses() {

            // Realizar a requisição
            const response = await this.$http.get('http://localhost:3000/api/v1/warehouses');

            // Extrair o JSON
            const result = await response.json();

            // Adicionar os dados de result no Array warehouses:
            this.warehouses = result;
            // return this.warehouses
        }
    }
}
</script>

<style>

</style>
