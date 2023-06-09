<template>
  <div class="form_container">
    <div class="form_label">
      COMPANY<div class="colored">ADDRESS</div>
    </div>
    <form @submit.prevent="registerAddress">
      <div class="mb-3">
        <label for="streetInput" class="form-label">Street</label>
        <input type="text" class="form-control" id="streetInput" v-model="street" required>
      </div>
      <div class="mb-3">
        <label for="cityInput" class="form-label">City</label>
        <input type="text" class="form-control" id="cityInput" v-model="city" required>
      </div>
      <div class="mb-3">
        <label for="stateInput" class="form-label">State</label>
        <input type="text" class="form-control" id="stateInput" v-model="state" required>
      </div>
      <div class="mb-3">
        <label for="cepInput" class="form-label">CEP</label>
        <input type="text" class="form-control" id="cepInput" v-model="cep" required>
      </div>
      <div class="button">
        <button type="submit" class="btn_primary">Register</button>
        <button type="button" class="btn_primary" @click="editAddress">Edit</button>
        <button type="button" class="btn_primary" @click="deleteAddress">Exclude</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      street: '',
      city: '',
      state: '',
      cep: ''
    };
  },
  methods: {
    async registerAddress(event) {
      event.preventDefault();
      const empresaId = this.$route.params.id; // Obtém o valor de id da rota
      try {
        const response = await fetch(`http://localhost:3000/enderecos`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            rua: this.street,
            cidade: this.city,
            estado: this.state,
            cep: this.cep,
          }),
        });

        if (response.ok) {
          console.log('Endereço registrado com sucesso!');
        } else {
          console.error('Erro ao registrar endereço:', response.statusText);
          console.error('Detalhes do erro:', await response.text());
        }
      } catch (error) {
        console.error('Erro ao conectar com o servidor:', error);
      }
    },
    editAddress() {
      
    },
    deleteAddress() {
      
    }
  }
};
</script>


  
<style scoped>
.form-label {
  font-size: 18px;
  font-weight: 700;
  display: flex;
}

.colored {
  margin-left: .5rem;
  background: linear-gradient(to bottom, #fd5949, #285AEB);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.form_label {
  padding-top: .5rem;
  padding-bottom: 1rem;
  font-size: 30px;
  font-weight: 700;
  display: flex;
}

.form_container {
  padding-top: 2rem;
  margin: auto;
  max-width: 50%;
  color: #ccc;
}

.button {
  margin-top: 2rem;
  display: flex;
  justify-content: center;
}

.btn_primary {
  background: linear-gradient(to bottom, #fd5949, #285AEB);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 600;
  color: #fff;
  box-shadow: none;
  margin: 1rem;
  transition: .2s ease;
  border: 1px solid;
  border-image: linear-gradient(to bottom, #fd5949, #285AEB) 1;
  border-image-slice: 1;
  border-radius: 8px;
}

.btn_primary:hover {
  filter: brightness(75%);
}
</style>