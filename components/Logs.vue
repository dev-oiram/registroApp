<template>
    <div>
      <b-table striped hover :items="tableData" :fields="tableFields"></b-table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        tableData: [],
        tableFields: [
          { key: 'id', label: 'ID' },
          { key: 'fecha', label: 'Fecha' },
          { key: 'mensaje', label: 'Mensaje' },
        ]
      };
    },
    mounted() {
      this.fetchData();
    },
    methods: {
      async fetchData() {
        try {
          const response = await this.$axios.get('/logs');
          this.tableData = response.data;
        } catch (error) {
          console.error(error);
        }
      }
    }
  };
  </script>
