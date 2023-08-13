<template>
  <header>
    <nav>
      <ul>
        <li class="header-home" @click="changePage('HomeSearch')">Home</li>
        <li class="header-enderecos" @click="changePage('EnderecoSalvo')">Endereços Salvos</li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  data() {
    return {
      currentPage: String
    };
  },
  methods: {
    changePage(page) {
      this.$emit('page-change', page);
    }
  }
};
</script>

<style scoped>
header {
  padding: 1rem;
  text-align: right;
  background-color: #34495E;
}

ul {
  display: flex;
}

li {
  text-decoration: none;
  display: flex;
  flex-direction: row;
  text-decoration: none;
  cursor: default;
}
li:hover{
  background-color: white;
  color: black;
}

.header-home,
.header-enderecos {
  text-decoration: none;
  padding: 20px;
  text-align: right;
  color: white;
  font-weight: 500;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

</style>
