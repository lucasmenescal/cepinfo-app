<template>
  <div class="card" @click="openModal">
    <div class="info-endereco">
      <h3>{{ endereco.cep }}</h3>
      <p>{{ endereco.logradouro }}</p>
    </div>
    <div class="butons">
      <button class="edit-button" @click="editarModal">Editar</button>
      <button class="delete-button" @click="openYesNoModal">Deletar</button>
    </div>
    <YesNoModal :showModal="showYesNoModal" :enderecoCep="endereco.cep" @fechar-modal="fecharYesNoModal" />

    <EditarEnderecoModal :show-modal="showEditarModal" :endereco-json="endereco" @fechar-modal="fecharEditarModal" />
  </div>
</template>
<script>
import YesNoModal from './messages/ModalYesNo.vue';
import EditarEnderecoModal from './EditarEnderecoModal.vue';
export default {
  components: {
    YesNoModal,
    EditarEnderecoModal
  },
  data() {
    return {
      showYesNoModal: false,
      showEditarModal: false
    }
  },
  props: {
    endereco: Object
  },
  methods: {
    fecharModais(){
      this.fecharEditarModal();
    },
    editarModal() {
      this.showEditarModal = true;
    },
    fecharEditarModal() {
      this.showEditarModal = false;
    },
    fecharYesNoModal() {
      this.showYesNoModal = false;
    },
    openYesNoModal() {
      this.showYesNoModal = true;
    },
    openModal() {
      this.$emit('open-modal', this.endereco);
    },
    async editar() {
      const updateUrl = `http://localhost:8000/enderecos/update`;

      try {
        const response = await fetch(updateUrl, {
          method: 'PUT', // Use 'PATCH' ou 'PUT' dependendo da sua API
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(this.endereco)
        });

        if (response.status === 200) {
          // Atualizar o endereço localmente ou emitir um evento para atualização
          // Por exemplo:
          // this.$emit('endereco-atualizado', response.json());
        } else {
          console.error('Erro ao atualizar endereço:', response.statusText);
        }
      } catch (error) {
        console.error('Erro ao atualizar endereço:', error);
      }
    },

  }
};
</script>

<style scoped>
.card {
  align-items: center;
  color: white;

  display: flex;
  flex-direction: row;
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px;
  justify-content: space-between;

}

h3,
p {
  padding: 10px;
  margin: 10px;

}

.info-endereco,
.butons {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.edit-button,
.delete-button {
  border-radius: 5px;
}

button {
  padding: 10px;
  font-size: 20px;
  margin: 5px;
  border-radius: 0;
  border: 1px solid black;
  background-color: white;
}

button:hover {
  background-color: black;
  color: white;
}

.card:hover {
  background-color: white;
  color: black;

}

@media screen and (max-width: 415px) {

  /* Max-width para iPhone XR */
  .card {
    padding: 0;
  }

  .buttons {
    font-size: 10px;
    /* Tamanho menor para telas menores */
    padding: 0;
    margin: 0;
    border: 1px solid black;
  }

  button:hover {
    background-color: black;
    color: white;
  }

  h3,
  p {
    font-size: 15px;
    padding: 2px;
    margin: 2px;
  }

  .card:hover {
    background-color: white;
    color: black;
  }

}
</style>
