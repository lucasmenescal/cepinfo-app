<template>
  <div class="card" @click="openModal">
    <h3>{{ endereco.cep }}</h3>
    <p>{{ endereco.logradouro }}</p>

  </div>
</template>

<script>
export default {
  props: {
    endereco: Object
  },
  methods: {
    openModal() {
      this.$emit('open-modal', this.endereco);
    }
  }
};
</script>

<style scoped>
.card {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px;
}

.card:hover {
  background-color: white;
}
</style>
