<template>
  <div class="modal-overlay" v-show="showModal">
    <div class="modal">
      <h2>Endereço</h2>
      <div v-if="enderecoJson" class="input-container" v-bind="enderecoJsonSave = enderecoJson">
        <div class="input-row">
          <label for="cep">CEP:</label>
          <input v-model="enderecoJsonSave.cep" type="text">
        </div>
        <div class="input-row">
          <label for="logradouro">Logradouro:</label>
          <input v-model="enderecoJsonSave.logradouro" type="text">
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

        <div class="butons">
          <button class="save-button" @click="update">Salvar</button>
          <button class="close-button" @click="fecharEditarModal">Cancelar</button>

          <MessageModal :show-modal="showMessageModal" :message="message" @fechar-modais="fecharModais" />
          <ErrorModal :show-modal="showErrorModal" :error-message="errorMessage" @fechar-modal="fecharErroModal" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import ErrorModal from './messages/ErrorModal.vue';
import MessageModal from './messages/MessageModal.vue';

export default {
  name: 'EditarEnderecoModal',
  components: {
    ErrorModal,
    MessageModal
  },
  props: {
    showModal: Boolean,
    enderecoJson: Object,
    endereco: Object,
  },
  emits: ['fechar-modal', 'fechar-modais'],

  methods: {
    async update() {
      const updateUrl = `http://localhost:8000/enderecos/update`;
      try {
        const response = await fetch(updateUrl, {
          method: 'PUT',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(this.enderecoJsonSave)
        });

        if (response.status === 200) {
          this.showMessageModal = true;
          this.message = "Endereço atualizado com sucesso!";
        } else {
          console.error('Erro ao atualizar endereço:', response.statusText);
        }
      } catch (error) {
        console.error('Erro ao atualizar endereço:', error);
        this.showErrorModal = true;
        this.errorMessage = 'Erro ao atualizar endereço!';
      }
    },

    fecharModais() {
      this.$emit('fechar-modal');
      this.$emit('fechar-modais');
      location.reload();
    },
    fecharEditarModal() {
      this.$emit('fechar-modal');
    },
    atualizarValor(chave, valor) {
      this.$emit('atualizar-valor', chave, valor);
    },
    
    fecharErroModal() {
      this.showErrorModal = false;
      this.errorMessage = null;
    },
    fecharMessageModal() {
      this.showMessageModal = false;
      this.message = null;
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
        siafi: ''
      },
      showErrorModal: false,
      errorMessage: '',
      message: '',
      showMessageModal: false
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
  padding: 10px 5px;
  font-size: 20px;
  margin: 10px;
  border: 1px solid black;
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


@media screen and (max-width: 415px) {

  .butons {
    font-size: 10px;
    padding: 2px;
    margin: 2px;
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
    margin-right: 5px;
    font-size: 15px;
    font-weight: bold;
    flex-shrink: 0;
  }

  .input-row input {
    padding: 4px;
    font-size: 15px;
    width: 100%;
  }
}
</style>