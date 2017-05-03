<template>
  <div>
    <div class="cep-container">
      <h2>Digite o CEP no campo abaixo</h2>
      <input type="text" size="11" maxlength="9" placeholder="00000-000" v-on:keyup="search" v-model="cep">
    </div>

    <div class="address-container">
      <div v-if="found">
        <h3>Endereço encontrado:</h3>
        <p>
          <span>Logradouro: {{ address.logradouro }}</span>
          <span>Complemento: {{ address.complemento }}</span>
          <span>Bairro: {{ address.bairro }}</span>
          <span>Localidade: {{ address.localidade }} - Etado: {{ address.uf }}</span>
        </p>
      </div>

      <div v-else-if="error">
        <p class="error">{{ error }}</p>
      </div> 

      <div v-else>
        <p>Aguardando endereço</p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        cep: '',
        found: false,
        address: {},
        error: ''
      }
    },

    methods: {
      search() {
        if (this.cep.length === 5) {
          this.cep = this.cep + '-'
        }

        if (/^[0-9]{5}-[0-9]{3}/.test(this.cep)) {
          fetch('https://viacep.com.br/ws/' + this.cep + '/json')
            .then((response) => {
              return response.json()
            })
            .then((response) => {
              if (response.erro) {
                throw new Error('Address not found')
              } else {
                this.address = response
                this.found = true
              }
            })
            .catch((err) => {
              this.error = 'Endereço não encontrado'
            })
        } else {
          this.found = false
          this.error = ''
          this.address = {}
        }
      }
    }
  }
</script>

<style scoped>
  .cep-container {
    width: 90%;
    background: #F4F4F4;
    border: 1px solid #ddd;
    border-radius: 5px;
    margin: 0 auto;
    padding: 1em;
  }

  h2 {
    font-size: 1em;
  }

  input[type=text] {
    font-size: 1em;
    text-align: center;
    color: #41B883;
    padding: 0.4em;
  }

  .address-container {
    width: 90%;
    margin: 0 auto;
    padding: 1em;
  }

  .address-container p span {
    display: block;
  }

  .address-container .error {
    color: #c03;
  }
</style>