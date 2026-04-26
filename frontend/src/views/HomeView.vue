<template>
  <router-link to="/login" class="text-primary text-decoration-none font-weight-bold">
                  Inicia sesión aquí
  </router-link>
  <br>
  <br>
  <router-link to="/registro" class="text-primary text-decoration-none font-weight-bold">
                  Registrarse
  </router-link>

  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "HomeView",
  components: {
    HelloWorld,
  },
};
</script>
