<template>
  <div id="app">
    <Header></Header>
    <Navbar></Navbar>
    <div class="view-container">
      <router-view />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue"
import Navbar from "./components/Navbar.vue"

export default {
  name: 'App',
  data() {
    return {
      headerTitle: "Usuários"
    }
  },
  components: {
    Header,
    Navbar,
  }
}
</script>

<style>
/* SINTA-SE A VONTADE PARA ALTERAR ESSAS ESTILIZAÇÕES BASICAS */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}

:root {
  --brand-magenta: #e02b57;
  --brand-magenta-light: #f6678d;
  --brand-magenta-dark: #c7264e;
  --paragraph: #7e7e7e;
}

.modal {
  z-index: 10;
}
</style>
