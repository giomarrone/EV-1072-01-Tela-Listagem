<template>
  <div id="app">
    <div class="view-container">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      headerTitle: "Usuários"
    }
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
  --brand-magenta-hover: #f84773;
  --brand-magenta-light: #fddfe8;
  --brand-magenta-dark: #c7264e;
  --paragraph: #7e7e7e;
  /* font-size: 62.5%; */
}

.modal {
  z-index: 10;
}
</style>
