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
        <div class="input-area">
          <label for="birthday-input">Data de nascimento:</label>
          <input
            maxlength="10"
            type="text"
            v-model="birthday"
            v-mask="'##/##/####'"
          />
        </div>
      <div class="input-area">
        <label for="phone-input">Telefone:</label>
        <input
          maxlength="15"
          type="text"
          v-model="phone"
          v-mask="'(##) #####-####'"
        />
      </div>
      <div class="input-area">
        <label for="contact-input">Contato:</label>
        <select name="contactOptions" id="contact" v-model="contact">
          <option value="Whatsapp">Whatsapp</option>
          <option value="E-mail">E-mail</option>
          <option value="SMS">SMS</option>
        </select>
      </div>
      <div class="input-area">
        <label for="contact-input">E-mail:</label>
        <input
          type="text"
          v-model="email"
        />
      </div>
      <button  id="submit-btn" type="button" @click="validadeForm()">
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
      birthday: "",
      phone: "",
      email: "",
      userName: "",
      contact: ""
    };
  },

  methods: {
    validadeForm() {
      if (!this.userName) {
        alert("Preencha o campo de nome.");
      } else if (!this.cpf || this.cpf.length < 11) {
        alert("Informe o CPF completo do usuário.");
      } else if (!this.birthday || this.birthday.length < 8) {
        alert("Informe a data de nascimento do usuário.");
      } else if (!this.phone || this.phone.length < 11) {
        alert("Informe o número do telefone do usuário.");
      } else if (!this.email || this.email.length == 0) {
        alert("Informe o e-mail do usuário.");
      }else this.postUser();
    },
    postUser() {
      axios
        .post("/api/users", { fullname: this.userName, cpf: this.cpf, phone: this.phone, email: this.email, birthDate: this.birthday, contact: this.contact })
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
  margin-bottom: 4rem;
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
  gap: 2rem;
  align-items: center;
  justify-content: space-between;
}

.input-area input, .input-area select {
  width: 70%;
  padding: 0.5rem;
  border-radius: 0.5rem;
  border: none;
  background-color: #f5f5f5;
}

.input-area label {
  width: 30%;
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
