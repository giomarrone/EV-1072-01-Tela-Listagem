<template>
  <table id="table" class="">
    <tr class="head-tr">
      <th>CPF</th>
      <th>Nome Completo</th>
      <th></th>
    </tr>
    <tr v-bind:id="user.id" v-for="user in dataUsers.reverse().slice(countOrigin, countEnd)" :key="user.id">
      <td class="cpf" id="cpf">
        {{ user.cpf }}
      </td>
      <td class="name" id="name">{{ user.fullname }}</td>
      <td class="eye-btn">
        <button id="eye-btn" @click="hideUser(user.id)">
          <img
            class="display-none"
            id="closed-eye"
            src="../assets/hideen-eye.svg"
            alt="ícone olho fechado"
          />
          <img src="../assets/details-eye.svg" id="eye" alt="ícone olho" />
        </button>
      </td>
    </tr>
  </table>
</template>

<script>
import axios from "axios";

export default {
  name: "UsersList",

  data() {
    return { dataUsers: [], cpf: "", countOrigin: 0, countEnd: 5};
  },

  methods: {
    hideUser(id) {
      const user = document.getElementById(id);
      const cpf = user.childNodes[0];
      const name = user.childNodes[1];
      cpf.classList.toggle("hide");
      name.classList.toggle("hide");
      const button = user.childNodes[2];
    },
  },

  mounted() {
    axios
      .get("http://localhost:8080/api/users")
      .then((response) => {
        this.dataUsers = response.data.users;
        console.log(response);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style scoped>
table {
  margin: 0 auto;
  border-collapse: collapse;
  width: 48rem;
  margin-top: 1rem;
  margin-bottom: 7rem;
}

th {
  text-align: left;
  padding: 1rem 2rem;
  border-top: 1px solid #c7c7c7;
  border-bottom: 1px solid #c7c7c7;
}

.display-none {
  display: none;
}

.message {
  background-color: aqua;
  width: 46rem;
}

.cpf {
  width: 11rem;
}

.eye-btn {
  display: flex;
  justify-content: flex-end;
}

.eye-btn button {
  /* background-color: transparent; */
  border: 1px solid transparent;
  padding: 0.2rem;
  background-color: transparent;
  transition: 0.2s;
  border-radius: 1rem;
  cursor: pointer;
}

.eye-btn button:hover {
  transition: 0.2s;
  background-color: #ffe5ec;
  border: 1px solid var(--brand-magenta);
}

.eye-btn button img {
  vertical-align: bottom;
}

.hide {
  filter: blur(5px);
}

td {
  padding: 1rem 2rem;
}

tr {
  transition: .2s ease-out;
}

tr:hover {
  background-color: #f4f4f4;
}

.head-tr {
  user-select: none;
}

.head-tr:hover {
  background-color: transparent;
}
</style>
