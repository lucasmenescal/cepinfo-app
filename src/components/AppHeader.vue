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
  padding: 0;
  margin: 0;
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
  padding: 5px 10px;
  text-align: right;
  color: white;
  font-weight: 500;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

@media screen and (max-width: 415px) {
  header{
    display: flex;
    margin: 0;

    font-size: 20px;
  }
  
}

</style>
