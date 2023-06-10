<template>
    <div>
      <b-table striped hover :items="tableData" :fields="tableFields"></b-table>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        tableData: [],
        tableFields: [
          { key: 'id', label: 'ID' },
          { key: 'nombre', label: 'Nombre' },
          { key: 'datosContacto.correo', label: 'Correo' },
          { key: 'datosContacto.telefono', label: 'Teléfono' },
        ]
      };
    },
    mounted() {
      this.fetchData();
    },
    methods: {
        async fetchData() {
            try {
                const response = await this.$axios.get('/usuarios');
                this.tableData = response.data
            } catch (error) {
                console.error(error);
            }
        }
    }
  };
  </script>
