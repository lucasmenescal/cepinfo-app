<template>
  <div class="modal-overlay" v-show="showModal">
    <div class="modal">
      <p>Deseja realmente apagar o CEP?</p>
      <button class="close-button" @click="deletar">Sim</button>
      <button class="close-button" @click="fecharModais">Não</button>
      <MessageModal :show-modal="showMessageModal" :message="message" @fechar-modais="fecharModais" />
    </div>
  </div>
</template>

<script>
import MessageModal from './MessageModal.vue';
export default {
  name: 'ModalYesNo',
  components: {
    MessageModal
  },
  data() {
    return {
      showMessageModal: false,
      message: ''
    }
  },
  props: {
    showModal: Boolean,
    enderecoCep: String,
  },
  methods: {
    fecharMessageModal() {
      this.showMessageModal = false;
    },
    async deletar() {
      const deleteUrl = `http://localhost:8000/enderecos/delete/${this.enderecoCep}`;
      try {
        const response = await fetch(deleteUrl, {
          method: 'DELETE',
          headers: {
            'Content-Type': 'application/json'
          }
        });
        if (response.status === 200) {
          this.showMessageModal = true;
          this.message = "Endereço deletado com sucesso";
        }
      } catch (error) {
        console.error('Erro ao deletar endereço:', error);
      }
    },
    fecharModais() {
      this.fecharModalYesNo();
      this.$emit('fechar-modais');
    },
    fecharModalYesNo() {
      this.$emit('fechar-modal');
    }
  }
};
</script>

<style>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  background-color: white;
  padding: 15px 50px;
  margin: 15px 50px;
  border-radius: 5px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2);
  text-align: center;
}

.close-button {
  padding: 5px 10px;
  font-size: 16px;
  border: none;
  background-color: #ddd;
  border-radius: 5px;
  cursor: pointer;
}
</style>
