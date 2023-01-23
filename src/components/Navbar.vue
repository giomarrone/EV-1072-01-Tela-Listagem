<template>
  <div id="nav-container" class="nav-container">
    <ul class="selected-area">
      <router-link to="/register" class="tab">
        CADASTRO
      </router-link>
      <router-link to="/" class="tab">
        LISTAGEM
      </router-link>
    </ul>
    
  </div>
</template>

<script>
import router from "@/router";

export default {
  name: "Navbar",

  data() {
    return {
      dataUsers: [],
    };
  },

  props: {
    tab: String
  },

  components: { router },
};
</script>

<style scoped>
.display-none {
  display: none;
}
.nav-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 48rem;
  margin: 0 auto;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.selected-area {
  display: flex;
  margin: 0 auto;
  justify-content: center;
  margin-top: 7rem;
}

button {
  cursor: pointer;
}

.tab {
  width: 10rem;
  height: 2.5rem;
  text-align: center;
  list-style: none;
  background-color: transparent;
  color: var(--paragraph);
  font-weight: 700;
  font-size: 1rem;
  border: none;
  transition: 0.2s;
  user-select: none;
  text-decoration: none;
}

a.router-link-exact-active {
  transition: 0.2s;
  border-bottom: 2px solid black;
  color: black;
}
</style>
