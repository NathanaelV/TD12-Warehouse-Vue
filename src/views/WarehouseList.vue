<template>
    <div>
        <h1>Galpões Cadastrados</h1>
    </div>
</template>

<script>
export default {
    name: 'WarehouseList',

    async mounted() {
        this.getWarehouses();
    },

    methods: {
        async getWarehouses() {

            // Realizar a requisição
            const response = await this.$http.get('http://localhost:3000/api/v1/warehouses');

            // Extrair o JSON
            const result = await response.json();

            console.log(result);
        }
    },
}
</script>

<style>

</style>
