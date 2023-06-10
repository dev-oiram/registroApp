<template>
    <div class="registration-form">
      <b-form @submit="submitForm" ref="form">
  
        <h3>Información Personal</h3>
        <div class="row">
          <div class="col-md-12">
            <b-form-group
              id="input-name"
              label="Nombre"
              label-for="name-input"
            >
              <b-form-input
                id="name-input"
                v-model="nombre"
                required
              ></b-form-input>
            </b-form-group>
          </div>
        </div>
  
        <h3>Información de Contacto</h3>
        <div class="row">
          <div class="col-md-6">
            <b-form-group
              id="input-telefono"
              label="Teléfono"
              label-for="telefono-input"
            >
              <b-form-input
                id="telefono-input"
                v-model="telefono"
                type="number"
                required
              ></b-form-input>
            </b-form-group>
          </div>
          <div class="col-md-6">
            <b-form-group
              id="input-email"
              label="Correo electrónico"
              label-for="email-input"
            >
              <b-form-input
                id="email-input"
                v-model="correo"
                type="email"
                required
              ></b-form-input>
            </b-form-group>
          </div>
        </div>
  
        <h3>Contraseña</h3>
        <div class="row">
          <div class="col-md-6">
            <b-form-group
              id="input-password"
              label="Contraseña"
              label-for="password-input"
            >
              <b-form-input
                id="password-input"
                v-model="contrasena"
                type="password"
                :state="contrasenaValida ? true : false"
                required
              ></b-form-input>
              <b-form-invalid-feedback :state="!contrasenaValida">
                {{ contrasenaValida ? 'Válida' : 'Debe tener al menos 10 caracteres, una mayúscula, una minúscula, un número y un símbolo.' }}
              </b-form-invalid-feedback>
            </b-form-group>
          </div>
          <div class="col-md-6">
            <b-form-group
              id="input-confirm-password"
              label="Confirmar contraseña"
              label-for="confirm-password-input"
            >
              <b-form-input
                id="confirm-password-input"
                v-model="confirmarContrasena"
                type="password"
                :state="confirmarContrasena === contrasena"
                required
              ></b-form-input>
              <b-form-invalid-feedback :state="confirmarContrasena === contrasena">
                {{ confirmarContrasena === contrasena ? 'Coinciden' : 'Las contraseñas no coinciden.' }}
              </b-form-invalid-feedback>
            </b-form-group>
          </div>
        </div>
  
        <b-button type="submit" variant="primary">Registrarse</b-button>
      </b-form>
    </div>
  </template>
  
  <script>
  import Swal from 'sweetalert2';

  export default {
    data() {
      return {
        nombre: '',
        correo: '',
        formValid: false,
        telefono: '',
        contrasena: '',
        confirmarContrasena: ''
      };
    },
    computed: {
      contrasenaValida() {
        const regex = /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[!@#$%^&*()\-_=+{};:,<.>]).{10,15}$/;
        this.formValid = regex.test(this.contrasena);
        return this.formValid
      }
    },
    methods: {
      procesoExitoso() {
        this.nombre = ''
        this.correo = '',
        this.formValid = false,
        this.telefono = '',
        this.contrasena = '',
        this.confirmarContrasena = ''

        Swal.fire({
            title: 'Exito!',
            text: 'Se agrego el registro correctamente',
            icon: 'success',
        });
      },
      async submitForm(event) {
        event.preventDefault(); // Prevenir un submit
        if (this.formValid && this.contrasena == this.confirmarContrasena) {
            try {
                const data = {
                    cliente: {
                        nombre: this.nombre
                    },
                    datosContacto: {
                        telefono: this.telefono,
                        correo: this.correo
                    },
                    claves: {
                        pass: this.contrasena
                    }
                }
                const response = await this.$axios.post('/usuarios', data);
                this.procesoExitoso()
            } catch (error) {
                Swal.fire({
                    title: 'Error!',
                    text: 'Ocurrio un problema al registrarse.',
                    icon: 'error',
                });
            }
        } else {
            Swal.fire({
                title: 'Aviso!',
                text: 'Corregir los errores en el registro',
                icon: 'warning',
            });
        }
      }
    }
  };
  </script>
  
  <style>
  .registration-form {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  </style>
