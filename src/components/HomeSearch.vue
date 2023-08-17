<template>
  <div class="home">
    <label for="home-search"></label>
    <input v-model="enderecoValue" class="home-search" type="text">
    <div class="buttons">
      <button class="home-button" @click="toggleModal(false)">Pesquisar</button>
      <button class="home-button" @click="toggleModal(true)">Novo Endereço</button>
    </div>
  </div>
  <ErrorModal :show-modal="showErrorModal" :error-message="errorMessage" @fechar-modal="fecharErroModal" />

  <EnderecoModal :show-modal="showModal" :endereco-json="enderecoJson" @fechar-modal="fecharEnderecoModal" />
</template>

<script>
import EnderecoModal from './EnderecoModal.vue';
import ErrorModal from './messages/ErrorModal.vue';

export default {
  name: 'HomeSearch',
  components: {
    EnderecoModal,
    ErrorModal
  },
  data() {
    return {
      enderecoValue: '',
      enderecoJson: {},
      showModal: false,
      showErrorModal: false,
      errorMessage: ''
    };
  },
  methods: {
    toggleModal(isNew) {
      if (isNew) {
        this.enderecoValue = null;
        this.enderecoJson = null;
        this.enderecoJsonSave = null;
      }
      if (!isNew && !this.enderecoValue) {
        this.showErrorModal = true;
        this.errorMessage = 'Por favor, insira um endereço válido.';
        return;
      }
      this.showModal = !this.showModal;
      if (this.showModal) {
        if (!isNew) {
          this.buscarEndereco();
        }
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
    fecharEnderecoModal() {
      this.showModal = false;
      this.enderecoValue = null;
    },
    fecharErroModal() {
      this.showErrorModal = false;
      this.enderecoValue = null;
    },
    limparInputs() {
      this.enderecoJsonSave.cep = ''
      this.enderecoJsonSave.logradouro = ''
      this.enderecoJsonSave.complemento = ''
      this.enderecoJsonSave.bairro = ''
      this.enderecoJsonSave.localidade = ''
      this.enderecoJsonSave.uf = ''
      this.enderecoJsonSave.ibge = ''
      this.enderecoJsonSave.gia = ''
      this.enderecoJsonSave.ddd = ''
      this.enderecoJsonSave.siafi = ''
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

.home-search {
  border-radius: 10px;
}

.home-search,
.home-button {
  padding: 10px;
  font-size: 20px;
  margin: 10px;
}

@media screen and (max-width: 415) {}
</style>
