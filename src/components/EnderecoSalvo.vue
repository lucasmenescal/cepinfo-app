<template>
  <div>
    <h1>Endereços Salvos</h1>
    <div>
      <CardEndereco v-for="(endereco, index) in enderecos" :key="index" :endereco="endereco" @click="toggleModal(endereco)" />
    </div>
    <EnderecoModal :show-modal="showModal" :endereco-json="enderecoSelecionado" @fechar-modal="fecharModal" />
  </div>
</template>

<script>
import CardEndereco from './CardEndereco.vue';
import EnderecoModal from './EnderecoModal.vue';
export default {
  name: "EnderecoSalvo",
  components: {
    CardEndereco,
    EnderecoModal
  },
  data() {
    return {
      enderecos: [],
      enderecoSelecionado: null,
      showModal: false
    };
  },
  mounted() {
    this.fetchEnderecos();
  },
  methods: {
    toggleModal(endereco) {
      this.enderecoSelecionado = endereco;
      this.showModal = !this.showModal;
    },
    fetchEnderecos() {
      fetch('http://localhost:8000/enderecos/listarTudo')
        .then(response => response.json())
        .then(data => {
          this.enderecos = data;
        })
        .catch(error => {
          console.error('Erro ao buscar endereços:', error);
        });
    },
    fecharModal() {
      this.showModal = false;
      this.enderecoSelecionado = null;
    }
  }
};
</script>

<style></style>
