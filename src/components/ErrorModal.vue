<template>
  <div class="modal-overlay" v-show="showModal">
    <div class="modal">
      <p>{{ errorMessage }}</p>
      <button class="close-button" @click="fecharErrorModal">Fechar</button>
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'ErrorModal',
  props: {
    showModal: Boolean,
    errorMessage: String
  },
  methods: {
    fecharErrorModal() {
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
