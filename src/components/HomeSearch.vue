<template>
  <div class="home">
    <label for="home-search"></label>
    <input v-model="enderecoValue" class="home-search" type="text">
    <button class="home-button" @click="toggleModal">Pesquisar</button>
  </div>

  <EnderecoModal :show-modal="showModal" :endereco-json="enderecoJson" @fechar-modal="fecharModal" />

</template>

<script>
import EnderecoModal from './EnderecoModal.vue';
export default {
  name: 'HomeSearch',
  components: {
    EnderecoModal
  },
  data() {
    return {
      enderecoValue: '',
      enderecoJson: {},
      showModal: false
    };
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
      if (this.showModal) {
        this.buscarEndereco();
      }
    },
    buscarEndereco() {
      const url = `http://localhost:8000/enderecos/buscar/${this.enderecoValue}`;
      
      fetch(url)
        .then(response => response.json())
        .then(data => {
          this.enderecoJson = data;
        })
        .catch(error => {
          console.error('Erro na requisição:', error);
        });
    },
    fecharModal() {
      this.showModal = false;
    }
  }
};
</script>

<style scoped>
.home {
  height: 80vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.home-search{
  border-radius: 10px;
}

.home-search,
.home-button {
  padding: 10px;
  font-size: 20px;
  margin: 10px;
}

</style>
