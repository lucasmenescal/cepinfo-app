<template>
  <div id="app">
    <AppHeader class="header" @page-change="changePage" />
    <div>
      <Home v-if="currentPageComponent === 'HomeSearch'"/>
      <Enderecos v-if="currentPageComponent === 'EnderecoSalvo'"/>
    </div>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import Home from './components/HomeSearch.vue';
import Enderecos from './components/EnderecoSalvo.vue'

export default {
  components: {
    AppHeader,
    Home,
    Enderecos
  },
  data() {
    return {
      currentPage: 'HomeSearch'
    };
  },
  computed: {
    currentPageComponent() {
      return this.currentPage.charAt(0).toUpperCase() + this.currentPage.slice(1);
    }
  },
  methods: {
    changePage(page) {
      this.currentPage = page;
    }
  }
};
</script>

<style>
body {
  background-color: #6CA6CD;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}

.header {
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: row;
  justify-content: right;

  font-size: 30px;

}

@media screen and (max-width: 415) {
  .header{
    font-size: 20px;
  }
}
</style>
