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
          <input type="text">
        </div>
        <div class="input-row">
          <label for="logradouro">Logradouro:</label>
          <input type="text">
        </div>
        <div class="input-row">
          <label for="complemento">Complemento:</label>
          <input type="text">
        </div>
        <div class="input-row">
          <label for="bairro">Bairro:</label>
          <input type="text">
        </div>
        <div class="input-row">
          <label for="localidade">Localidade:</label>
          <input type="text">
        </div>
        <div class="input-row">
          <label for="uf">UF:</label>
          <input type="text">
        </div>
        <div class="input-row">
          <label for="ibge">IBGE:</label>
          <input type="text">
        </div>
        <div class="input-row">
          <label for="gia">GIA:</label>
          <input type="text">
        </div>
        <div class="input-row">
          <label for="ddd">DDD:</label>
          <input type="text">
        </div>
        <div class="input-row">
          <label for="siafi">siafi:</label>
          <input type="text">
        </div>
        <div class="input-row">
          <div class="input-columns"></div>
          <input type="text">
        </div>
      </div>
      <button class="close-button" @click="fecharModal">Fechar</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EnderecoModal',
  props: {
    showModal: Boolean,
    enderecoJson: Object,
    endereco: Object
  },
  methods: {
    fecharModal() {
      this.$emit('fechar-modal');
    },
    atualizarValor(chave, valor) {
      this.$emit('atualizar-valor', chave, valor);
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