<template>
  <div class="container my-5">
    <div class="row justify-content-center">
      <div class="col-12 col-md-8 col-lg-5">
        
        <div class="card shadow-lg border-0">
          <div class="card-body p-5">
            
            <div class="text-center mb-4">
              <h2 class="text-danger font-weight-bold">Burger & Fast Food</h2>
              <h4 class="text-muted">Crea tu cuenta nueva</h4>
            </div>

            <form @submit.prevent="procesarRegistro">
              
              <div class="form-group mb-3">
                <label class="form-label">Nombre completo</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="usuario.nombreCompleto"
                  placeholder="Ej: Alvaro Garcia"
                  required
                />
              </div>

              <div class="form-group mb-3">
                <label class="form-label">Correo electrónico</label>
                <input
                  type="email"
                  class="form-control"
                  v-model="usuario.correo"
                  placeholder="nombre@ejemplo.com"
                  required
                />
              </div>

              <div class="form-group mb-3">
                <label class="form-label">Contraseña</label>
                <input
                  type="password"
                  class="form-control"
                  v-model="usuario.contrasena"
                  placeholder="Crea una contraseña segura"
                  required
                />
                <div class="mt-2">
                  <small class="text-muted">Fortaleza: </small>
                  <span :class="claseColorFortaleza">{{ textoFortaleza }}</span>
                </div>
              </div>

              <div class="form-group mb-4">
                <label class="form-label">Confirmar contraseña</label>
                <input
                  type="password"
                  class="form-control"
                  v-model="usuario.confirmarContrasena"
                  placeholder="Repite tu contraseña"
                  required
                />
                <div v-if="contrasenasNoCoinciden" class="text-danger small mt-1">
                  Las contraseñas no coinciden.
                </div>
              </div>

              <button 
                type="submit" 
                class="btn btn-danger w-100 btn-lg font-weight-bold"
                :disabled="contrasenasNoCoinciden"
              >
                Crear cuenta
              </button>

            </form>

            <div class="text-center mt-4">
              <p class="mb-0">
                ¿Ya tienes cuenta? 
                <router-link to="/" class="text-primary text-decoration-none font-weight-bold">
                  Inicia sesión aquí
                </router-link>
              </p>
            </div>

          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "RegistroView",
  data() {
    return {
      usuario: {
        nombreCompleto: "",
        correo: "",
        contrasena: "",
        confirmarContrasena: ""
      }
    };
  },
  computed: {
    // Compara si las contraseñas son diferentes
    contrasenasNoCoinciden() {
      if (this.usuario.confirmarContrasena === "") return false;
      return this.usuario.contrasena !== this.usuario.confirmarContrasena;
    },
    // Lógica visual para el indicador de seguridad
    textoFortaleza() {
      const largo = this.usuario.contrasena.length;
      if (largo === 0) return "Vacía";
      if (largo < 6) return "Débil";
      if (largo < 10) return "Media";
      return "Fuerte";
    },
    claseColorFortaleza() {
      const largo = this.usuario.contrasena.length;
      if (largo < 6) return "text-danger";
      if (largo < 10) return "text-warning";
      return "text-success font-weight-bold";
    }
  },
  methods: {
    procesarRegistro() {
      // Validamos que coincidan antes de permitir el "envío"
      if (this.contrasenasNoCoinciden) {
        alert("Por favor, verifica que las contraseñas sean iguales.");
        return;
      }

      // Captura de datos lista para enviar al backend (Express)
      const datosParaEnviar = {
        nombre: this.usuario.nombreCompleto,
        email: this.usuario.correo,
        clave: this.usuario.contrasena
      };

      console.log("Datos de registro capturados:", datosParaEnviar);
      // Aquí iría tu petición fetch o axios hacia el backend
    }
  }
};
</script>

<style scoped>
/* Estilos opcionales para mejorar el aspecto del formulario */
.card {
  border-radius: 15px;
}
.form-control {
  border-radius: 8px;
  padding: 10px 15px;
}
.btn-danger {
  background-color: #e74c3c;
  border: none;
}
.btn-danger:hover {
  background-color: #c0392b;
}
</style>