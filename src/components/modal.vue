<template>
  <div class="container" id="modal">
    <div class="modal">
      <p class="modal-title">Detalhes do usuário</p>
      <button type="button" class="close-btn" @click="closeModal()">
        <img src="../assets/close.svg" alt="Fechar modal" />
      </button>
      <div class="modal-items">
        <div class="left-column">
          <div class="info-item">
            <p class="item-name">CPF</p>
            <p class="item-info">{{ user.fullname }}</p>
          </div>
          <div class="info-item">
            <p class="item-name">Nome completo</p>
            <p class="item-info">{{ user.cpf }}</p>
          </div>
          <div class="info-item">
            <p class="item-name">Data de nascimento</p>
            <p class="item-info">{{ user.birthDate }}</p>
          </div>
        </div>
        <div class="right-column">
          <div class="info-item">
            <p class="item-name">Celular</p>
            <p class="item-info">{{ user.phone }}</p>
          </div>
          <div class="info-item">
            <p class="item-name">Contato</p>
            <p class="item-info">{{ user.contact }}</p>
          </div>
          <div class="info-item">
            <p class="item-name">E-mail</p>
            <p class="item-info">{{ user.email }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "UserModal",

  props: {
    user: {
      type: "",
      require: true,
    },
  },

  data() {
    return {
      dataUsers: [],
      cpf: "",
    };
  },

  methods: {
    closeModal() {
      this.$emit("closeModal");
      // console.log("fechou modal");
    },
  },
};
</script>
<style scoped>
.container {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  background-color: rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(5px);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  background-color: white;
  padding: 2rem 2rem;
  width: fit-content;
  border-radius: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 3rem;
  position: relative;
}

.modal-title {
  font-size: 1rem;
  font-weight: 700;
  text-align: center;
}

.modal-items {
  display: flex;
  gap: 7rem;
  background-image: repeating-linear-gradient(
      21deg,
      #cfcfcf,
      #cfcfcf 12px,
      transparent 12px,
      transparent 20px,
      #cfcfcf 20px
    ),
    repeating-linear-gradient(
      111deg,
      #cfcfcf,
      #cfcfcf 12px,
      transparent 12px,
      transparent 20px,
      #cfcfcf 20px
    ),
    repeating-linear-gradient(
      201deg,
      #cfcfcf,
      #cfcfcf 12px,
      transparent 12px,
      transparent 20px,
      #cfcfcf 20px
    ),
    repeating-linear-gradient(
      291deg,
      #cfcfcf,
      #cfcfcf 12px,
      transparent 12px,
      transparent 20px,
      #cfcfcf 20px
    );
  background-size: 1px 100%, 100% 1px, 1px 100%, 100% 1px;
  background-position: 0 0, 0 0, 100% 0, 0 100%;
  background-repeat: no-repeat;
  padding: 3rem;
}

.left-column,
.right-column {
  display: flex;
  flex-direction: column;
  width: 50%;
  gap: 1.5rem;
}

.info-item {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.item-name {
  color: rgb(141, 141, 141);
}

.item-info {
  font-size: 1.2rem;
  font-weight: 700;
}

.close-btn {
  position: absolute;
  right: 2rem;
  top: 1.7rem;
  background-color: transparent;
  border: none;
  cursor: pointer;
  transition: 0.2s;
}

.close-btn img {
  vertical-align: bottom;
}

.close-btn:hover {
  background-color: transparent;
  border: none;
  transition: 0.2s;
  transform: scale(1.2);
}
</style>
