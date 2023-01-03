<template>
  <div class="form-container">
    <form id="form" action="">
      <div class="input-area">
        <label for="name-input">Nome completo:</label>
        <input type="text" id="name-input" v-model="userName" />
      </div>
      <div class="input-area">
        <label for="cpf-input">CPF:</label>
        <input
          maxlength="14"
          type="text"
          v-model="cpf"
          v-mask="'###.###.###-##'"
        />
      </div>
      <button id="submit-btn" type="button" @click="validadeForm()">
        Cadastrar usuário
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Register",
  data() {
    return {
      dataUsers: [],
      cpf: "",
      userName: "",
    };
  },

  methods: {
    validadeForm() {
      if(!this.userName) {
        alert("Preencha o campo de nome.")
      } else if(!this.cpf || this.cpf.length < 11) {
        alert("Informe o CPF completo do usuário.")
      } else (this.postUser())
    },
    postUser() {
      axios
        .post("/api/users", { fullname: this.userName, cpf: this.cpf })
        .then(() => {
          console.log("Usuário cadastrado com sucesso");
        })
        .catch((error) => {
          console.log(error);
        });

      this.$router.push("./");
      this.$root.$refs.A.changeScreen();
    },
  },
};
</script>

<style scoped>
.form-container {
  width: 60%;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
}
form {
  width: 70%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 1rem;
  margin-top: 2rem;
}

.input-area {
  display: flex;
  width: 100%;
  justify-content: space-between;
  align-items: center;
}

.input-area input {
  width: 70%;
  padding: 0.5rem;
  border-radius: 0.5rem;
  border: none;
  background-color: #f5f5f5;
}

.input-area input:focus {
  outline-color: var(--brand-magenta);
}

form button {
  padding: 1rem 2rem;
  background-color: var(--brand-magenta);
  border: none;
  border-radius: 0.5rem;
  color: white;
  font-weight: 700;
  align-self: flex-end;
  margin-top: 1rem;
  cursor: pointer;
}
</style>
