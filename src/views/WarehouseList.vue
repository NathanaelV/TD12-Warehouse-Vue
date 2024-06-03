<template>
    <div>
        <h1>Galpões Cadastrados</h1>

        <v-text-field label="Buscar galpão" placeholder="Buscar Galpão" v-model="term" class="my-5"></v-text-field>

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
        <!-- <div v-for="w in filterWarehouse" :key="w.id">
            <Warehouse
                :name       = "w.name"
                :code       = "w.code"
                :address    = "w.address"
                :city       = "w.city"
                :area       = "w.area"
            />
        </div> -->
        
        <v-card dark>
            <v-card-text>
                <WarehouseTable :warehouses="filterWarehouse"/>
            </v-card-text>
        </v-card>
    </div>
</template>

<script>
// Importa componente Warehouse
import Warehouse from '../components/Warehouse.vue';
import WarehouseTable from '../components/WarehouseTable.vue';

export default {
    name: 'WarehouseList',

    components: {
        Warehouse,
        WarehouseTable
    },

    data() {
        return {
            warehouses: [],
            term: ''
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
    },

    computed: {
        filterWarehouse() {
            return this.warehouses.filter(warehouse => {
                // console.log('Warehouse: ' + warehouse.name.toLowerCase())
                console.log('Warehouse: ' + this.term)
                return warehouse.name.toLowerCase().includes(this.term.toLocaleLowerCase());
            })
        }
    }
}
</script>

<style>
.form {
    margin-bottom: 20px;
}
</style>
