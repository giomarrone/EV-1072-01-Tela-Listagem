<template>
  <div class="container">
    <table id="table" class="">
      <tr class="head-tr">
        <th>CPF</th>
        <th>Nome Completo</th>
        <th></th>
      </tr>
      <tr v-bind:id="user.id" v-for="user in currentItems" :key="user.id">
        <td class="cpf" id="cpf">
          {{ user.cpf }}
        </td>
        <td class="name" id="name">{{ user.fullname }}</td>
        <td class="eye-btn">
          <button id="eye-btn" v-bind="user" @click="openModal(user)">
            <img
              class="display-none"
              id="closed-eye"
              src="../assets/hideen-eye.svg"
              alt="ícone olho fechado"
            />
            <img src="../assets/details-eye.svg" id="eye" alt="ícone olho" />
          </button>
          <UserModal id="modal" :user="currentUser" @closeModal="isModal = false" v-show="isModal"></UserModal>
        </td>
      </tr>
    </table>
    <div class="pages">
      <jw-pagination
        :items="dataUsers"
        :pageSize="5"
        @changePage="onChangePage"
        :maxPages="5"
        :labels="customLabels"
        :disableDefaultStyles="true"
      ></jw-pagination>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import UserModal from "../components/modal.vue";

const exampleItems = [...Array(5).keys()].map((i) => ({
  id: i + 1,
  name: "Item " + (i + 1),
}));

const customLabels = {
  first: "<<",
  last: ">>",
  previous: "<",
  next: ">",
};


export default {
  name: "UsersList",

  data() {
    return {
      dataUsers: [],
      currentItems: [],
      cpf: "",
      exampleItems,
      customLabels,
      currentUser: {},
      isModal: false
    };
  },

  components: {
    UserModal,
  },

  methods: {
    onChangePage(currentItems) { //atualiza a página com is itens atuais
      this.currentItems = currentItems;
    },

    async getUsers() { 
      try {
        await axios.get("http://localhost:8080/api/users").then((response) => {
          this.dataUsers = response.data.users;
          console.log(response);
        });
      } catch {
        console.log("teste");
      }
    },

    openModal(user) {  // Abre o modal respecífico do usuário clicado
      // console.log("abriu modal");
      this.currentUser = user
      // console.log(this.currentUser)
      this.isModal = true
    },
    closeModal() {
      this.$emit("closeModal")
    }
  },

  mounted() {
    this.getUsers();
  },
};
</script>

<style>
#modal {
  position: absolute;
  right: 0;
}
table {
  margin: 0 auto;
  border-collapse: collapse;
  width: 48rem;
  margin-top: 1rem;
  margin-bottom: 7rem;
  border-bottom: 1px solid #c7c7c7;
}

.pages {
  margin: 0 auto;
  width: 48rem;
  display: flex;
  justify-content: center;
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
  transition: 0.2s ease-out;
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

.pagination {
  display: flex;
  justify-content: center;
  list-style: none;
  gap: 0.5rem;
  font-weight: 500;
}

.pagination li {
  cursor: pointer;
  background-color: transparent;
  padding: .3rem .2rem;
  border-radius: 5px;
  font-weight: 700;
  color: #808080;
  border: 1px solid transparent;
  transition: 0.2s;
}

.pagination li a {
  width: 100%;
  height: 100%;
  border-radius: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.pagination li:hover {
  transition: 0.2s;
  background-color: #e8e8e8;
  color: black;
  font-weight: 700;
}

.pagination li.active {
  background-color: rgb(71, 71, 71);
  color: white;
}
</style>
