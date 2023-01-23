<template>
  <div class="container">
    <Header></Header>
    <Navbar></Navbar>
    <div class="form-container">
      <div class="introduction">
        <h2>Dados de contato</h2>
        <p>Informe os dados do usuário a ser cadastrado.</p>
      </div>
      <form id="form" action="">
        <div class="name-input-area">
          <label class="form-label" for="name-input">Nome completo</label>
          <input type="text" id="name-input" v-model="userName" />
        </div>
        <div class="columns">
          <div class="input-area">
            <label class="form-label" for="contact-input">E-mail</label>
            <img src="../assets/email-icon.svg" alt="Ícone de e-mail">
            <input type="text" v-model="email" class="input-with-icon" />
          </div>
          <div class="input-area">
            <label class="form-label" for="contact-input"
              >Confirmar e-mail</label
            >
            <img src="../assets/email-icon.svg" alt="Ícone de e-mail">
            <input type="text" v-model="confirmEemail" class="input-with-icon" />
          </div>
          <div class="input-area">
            <label class="form-label" for="cpf-input">CPF</label>
            <input
              maxlength="14"
              type="text"
              v-model="cpf"
              v-mask="'###.###.###-##'"
            />
          </div>
          <div class="input-area">
            <label class="form-label" for="phone-input">Telefone</label>
            <input
              maxlength="15"
              type="text"
              v-model="phone"
              v-mask="'(##) #####-####'"
            />
          </div>
          <div class="input-area">
            <label class="form-label" for="birthday-input"
              >Data de nascimento</label
            >
            <img src="../assets/calendar.svg" alt="Ícone de calendário">
            <input
              maxlength="10"
              type="text"
              v-model="birthday"
              v-mask="'##/##/##'"
              class="input-with-icon"
            />
          </div>
        </div>
        <p class="form-txt">
          Falta pouco! Só precisamos saber como podemos falar com você.
        </p>
        <p class="form-txt">Por onde você gostaria que entremos em contato?</p>
        <div class="contact-options">
          <div class="contact-option">
            <input type="checkbox" id="email-sms" name="email-sms" />
            <label class="checkbox-label" for="email-sms">E-mail e SMS</label>
          </div>
          <div class="contact-option">
            <input type="checkbox" id="whatsapp" name="whatsapp" />
            <label class="checkbox-label" for="whatsapp">WhatsApp</label>
          </div>
        </div>
      </form>
      <div class="submit-area">
        <button id="submit-btn" type="button" @click="validadeForm()">
          Salvar
        </button>
        <router-link to="/" id="submit-btn" class="return">
          Voltar
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import router from "@/router";
import axios from "axios";
import Header from "../components/Header.vue";
import Navbar from "../components/Navbar.vue";

export default {
  name: "Register",
  data() {
    return {
      dataUsers: [],
      cpf: "",
      birthday: "",
      phone: "",
      email: "",
      confirmEemail: "",
      userName: "",
      contact: "",
    };
  },

  components: {
    Header,
    Navbar,
    router,
  },

  methods: {
    validadeForm() {
      const whatsappOpt = document.querySelector("#whatsapp");
      const emailsmsOpt = document.querySelector("#email-sms");

      if (whatsappOpt.checked === true && emailsmsOpt.checked === true) {
        this.contact = "E-mail, SMS e Whatsapp";
      } else if (
        whatsappOpt.checked === true &&
        emailsmsOpt.checked === false
      ) {
        this.contact = "Whatsapp";
      } else if (
        whatsappOpt.checked === false &&
        emailsmsOpt.checked === true
      ) {
        this.contact = "E-mail e SMS";
      }

      if (!this.userName) {
        alert("Preencha o campo de nome.");
      } else if (!this.cpf || this.cpf.length < 11) {
        alert("Informe o CPF completo do usuário.");
      } else if (!this.birthday || this.birthday.length < 6) {
        alert("Informe a data de nascimento do usuário.");
      } else if (!this.phone || this.phone.length < 11) {
        alert("Informe o número do telefone do usuário.");
      } else if (!this.email || this.email.length == 0) {
        alert("Informe o e-mail do usuário.");
      } else if (this.email !== this.confirmEemail) {
        alert("Os e-mails informados não são iguais.");
      } else if (
        whatsappOpt.checked === false &&
        emailsmsOpt.checked === false
      ) {
        alert("Selecione pelo menos uma opção de contato.");
      } else this.postUser();
    },
    postUser() {
      axios
        .post("/api/users", {
          fullname: this.userName,
          cpf: this.cpf,
          phone: this.phone,
          email: this.email,
          confirmEemail: this.confirmEemail,
          birthDate: this.birthday,
          contact: this.contact,
        })
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
  /* width: 60%; */
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.introduction {
  width: 60%;
}
h2 {
  margin-bottom: 0.8rem;
}
form {
  width: 60%;
  align-self: center;

  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 1.5rem;
  margin-top: 2rem;
}

.form-txt {
  font-weight: 700;
  font-size: 0.9rem;
}

.columns {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  row-gap: 1.5rem;
}
.input-area, .name-input-area {
  position: relative;
  width: 48%;
}

.name-input-area {
  width: 100%;
}

.input-area input, .name-input-area input {
  border: 2px solid black;
  border-radius: 4px;
  position: relative;
  line-height: 1.5rem;
  height: 3rem;
  width: 100%;
  padding-inline: 1rem;
}

.input-area input.input-with-icon {
  padding-left: 2.5rem;
}

.input-area img {
  position: absolute;
  z-index: 2;
  top: 25%;
  left: 3%;
}
.form-label {
  position: absolute;
  top: -13%;
  font-size: 0.7rem;
  z-index: 1;
  left: 1rem;
  background-color: white;
  padding: 0 5px;
}
.contact-options {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}
.contact-option {
  display: flex;
  align-items: center;
  gap: 1rem;
  height: fit-content;
  padding: 0;
}

.contact-option input {
  border-radius: 4px;
  position: relative;
}

.checkbox-label {
  font-size: 1rem;
}

.submit-area {
  border-top: 1px solid rgb(209, 209, 209);
  width: 100%;
  display: flex;
  justify-content: center;
  padding-block: 1rem;
  margin-top: 3rem;
  gap: 1rem;
}

.submit-area button {
  padding: 1rem 2.5rem;
  background-color: var(--brand-magenta);
  border: none;
  border-radius: 0.5rem;
  color: white;
  font-weight: 700;
  cursor: pointer;
  transition: 0.2s;
}

.submit-area .return {
  padding: 1rem 2.5rem;
  background-color: transparent;
  text-decoration: none;
  font-size: 0.9rem;
  border: none;
  border-radius: 0.5rem;
  color: white;
  font-weight: 700;
  cursor: pointer;
  transition: 0.2s;
}

.submit-area button:hover {
  transition: 0.2s;
  background-color: var(--brand-magenta-hover);
}

.submit-area .return {
  background-color: transparent;
  color: var(--brand-magenta);
  transition: 0.2s;
}

.submit-area .return:hover {
  transition: 0.2s;
  background-color: var(--brand-magenta-light);
}
</style>
