<template>
  <div class="modal-overlay" v-show="showModal">
    <div class="modal">
      <h2>Endereço</h2>
      <div v-if="enderecoJson" class="input-container">
        <div class="input-row">
          <label for="cep">CEP:</label>
          <input :value="enderecoJson.cep" type="text">
        </div>
        <div class="input-row">
          <label for="logradouro">Logradouro:</label>
          <input :value="enderecoJson.logradouro" type="text">
        </div>
        <div class="input-row">
          <label for="complemento">Complemento:</label>
          <input :value="enderecoJson.complemento" type="text">
        </div>
        <div class="input-row">
          <label for="bairro">Bairro:</label>
          <input :value="enderecoJson.bairro" type="text">
        </div>
        <div class="input-row">
          <label for="localidade">Localidade:</label>
          <input :value="enderecoJson.localidade" type="text">
        </div>
        <div class="input-row">
          <label for="uf">UF:</label>
          <input :value="enderecoJson.uf" type="text">
        </div>
        <div class="input-row">
          <label for="ibge">IBGE:</label>
          <input :value="enderecoJson.ibge" type="text">
        </div>
        <div class="input-row">
          <label for="gia">GIA:</label>
          <input :value="enderecoJson.gia" type="text">
        </div>
        <div class="input-row">
          <label for="ddd">DDD:</label>
          <input :value="enderecoJson.ddd" type="text">
        </div>
        <div class="input-row">
          <label for="siafi">siafi:</label>
          <input :value="enderecoJson.siafi" type="text">
        </div>

      </div>
      <div v-else class="input-container">
        <div class="input-row">
          <label for="cep">CEP:</label>
          <input v-model="enderecoJsonSave.cep" type="text" required>
        </div>
        <div class="input-row">
          <label for="logradouro">Logradouro:</label>
          <input v-model="enderecoJsonSave.logradouro" type="text" required>
        </div>
        <div class="input-row">
          <label for="complemento">Complemento:</label>
          <input v-model="enderecoJsonSave.complemento" type="text">
        </div>
        <div class="input-row">
          <label for="bairro">Bairro:</label>
          <input v-model="enderecoJsonSave.bairro" type="text">
        </div>
        <div class="input-row">
          <label for="localidade">Localidade:</label>
          <input v-model="enderecoJsonSave.localidade" type="text">
        </div>
        <div class="input-row">
          <label for="uf">UF:</label>
          <input v-model="enderecoJsonSave.uf" type="text">
        </div>
        <div class="input-row">
          <label for="ibge">IBGE:</label>
          <input v-model="enderecoJsonSave.ibge" type="text">
        </div>
        <div class="input-row">
          <label for="gia">GIA:</label>
          <input v-model="enderecoJsonSave.gia" type="text">
        </div>
        <div class="input-row">
          <label for="ddd">DDD:</label>
          <input v-model="enderecoJsonSave.ddd" type="text">
        </div>
        <div class="input-row">
          <label for="siafi">siafi:</label>
          <input v-model="enderecoJsonSave.siafi" type="text">
        </div>

      </div>
      <div class="butons">
        <button class="close-button" @click="fecharModal">Fechar</button>
        <button v-if="!enderecoJson" class="save-button" @click="save()">Salvar</button>
      </div>
    </div>
  </div>

  <ErrorModal :show-modal="showErrorModal" :error-message="errorMessage" @fechar-modal="fecharErroModal" />
</template>

<script>
import ErrorModal from './ErrorModal.vue';
export default {
  name: 'EnderecoModal',
  components: {
    ErrorModal
  },
  props: {
    showModal: Boolean,
    enderecoJson: Object,
    endereco: Object,
  },
  emits: ['fechar-modal'],

  methods: {
    fecharModal() {
      this.$emit('fechar-modal');
    },
    atualizarValor(chave, valor) {
      this.$emit('atualizar-valor', chave, valor);
    },
    save() {
      if (!this.enderecoJsonSave.cep || !this.enderecoJsonSave.logradouro) {
        this.showErrorModal = true;
        this.errorMessage = 'CEP e logradouro nulo. Favor preencher';
        return;
      }
    },
    fecharErroModal() {
      this.showErrorModal = false;
      this.errorMessage = null;
    }
  },
  data() {
    return {
      enderecoJsonSave: {
        cep: '',
        logradouro: '',
        complemento: '',
        bairro: '',
        localidade: '',
        uf: '',
        ibge: '',
        gia: '',
        ddd: '',
        siafi: '',
      },
      showErrorModal: false,
      errorMessage: ''
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

.close-button,
.save-button {
  padding: 5px 10px;
  margin: 10px;
  font-size: 16px;
  border: none;
  background-color: #ddd;
  border-radius: 5px;
  cursor: pointer;
}

.input-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.input-row {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.input-row label {
  margin-right: 10px;
  font-weight: bold;
  flex-shrink: 0;
}

.input-row input {
  flex: 1;
  padding: 4px;
  font-size: 12px;
  width: 100%;
}
</style>