<template>
  <div id="app">
    <img src="./assets/logo.png" class="logo">
    <h1>{{ title }}</h1>

    <cc-cep></cc-cep>
  </div>
</template>

<script>
  import CcCep from './modules/cep/main.vue'

  export default {
    name: 'vueCep',

    data () {
      return {
        title: 'Vue CEP'
      }
    },

    components: {
      CcCep
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

.logo {
  width: 100px;
}

h1, h2 {
  font-weight: normal;
}

a {
  color: #42b983;
}
</style>
