<template>
  <div class=" aaa container d-flex justify-content-center align-items-center">
    <div class=" cinthia card shadow p-4">
      
      <div class="text-center mb-2-4">
        <h2 class="text-primary font-weight-bold">Restaurante de Comida Rapida</h2>
        <p class="text-muted">Inicia sesión en tu cuenta</p>
      </div>
      <form @submit.prevent="prepararEnvio">
        <div class="form-group mb-3">
          <label for="correo">Correo electrónico</label>
          <input
            type="email"
            id="correo"
            class="form-control"
            v-model="credenciales.correo"
            placeholder="ejemplo@correo.com"
            required
          />
        </div>

        <div class="form-group mb-4">
          <label for="contrasena">Contraseña</label>
          <div class="input-group">
            <input
              :type="tipoEntradaContrasena"
              id="contrasena"
              class="form-control"
              v-model="credenciales.contrasena"
              placeholder="Ingresa tu contraseña"
              required
            />
            <div class="input-group-append">
              <button
                class="btn btn-outline-secondary"
                type="button"
                @click="alternarVisibilidad"
              >
                {{ textoBotonVisibilidad }}
              </button>
            </div>
          </div>
        </div>

        <button type="submit" class="btn btn-primary btn-block w-100">
          Iniciar sesión
        </button>
        
      </form>

      <div class="text-center mt-4">
        <p class="mb-0">
          ¿No tienes cuenta? 
          <router-link to="/registro" class="text-decoration-none" >
            Regístrate aquí
          </router-link>
        </p>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: "LoginView",
  data() {
    return {
      credenciales: {
        correo: "",
        contrasena: ""
      },
      mostrarContrasena: false
    };
  },
  computed: {
    // Cambia dinámicamente el tipo de input entre "password" y "text"
    tipoEntradaContrasena() {
      return this.mostrarContrasena ? "text" : "password";
    },
    // Cambia dinámicamente el texto del botón
    textoBotonVisibilidad() {
      return this.mostrarContrasena ? "Ocultar" : "Mostrar";
    }
  },
  methods: {
    alternarVisibilidad() {
      this.mostrarContrasena = !this.mostrarContrasena;
    },
    prepararEnvio() {
      // Como acordamos, aquí no hay lógica de negocio.
      // Solo capturamos los datos de la vista listos para ser enviados a tu backend en Express.
      console.log("Datos capturados en el frontend:", this.credenciales);
      
      // Más adelante, aquí colocarás la llamada Axios/Fetch hacia tu API.
    }
  }
};
</script>

<style scoped>

.cinthia {
    background-color: #8FC3FA;
    width: 100%; max-width: 400px;
}

.aaa {
    background-color: #032344;
    width: 100%;
    min-height: 100vh;
}
/* El contenedor principal ocupa toda la altura (100vh) para centrar la tarjeta verticalmente.
   Si tuvieras estilos globales, aquí podrías agregar detalles extra específicos para el login. */
</style>