<template>
  <div class="text-center">
    <h3>Pagina Principal</h3>

    <b-tabs>
      <b-tab title="Registro" active>
        <Formulario />
      </b-tab>
      <b-tab title="Usuarios">
        <Usuarios />
      </b-tab>
      <b-tab title="Logs">
        Logs
      </b-tab>
    </b-tabs>

  </div>
</template>

<script>
import Formulario from '@/components/Formulario.vue';
import usuarios from '@/components/Usuarios.vue';

export default {
  data() {
    return {};
  },
  components: {
    Formulario,
    usuarios
  }
};
</script>
