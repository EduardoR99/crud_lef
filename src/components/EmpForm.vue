<template>
  <div class="form_container">
    <div class="form_label">
      Register your company
    </div>
    <form @submit.prevent="submitForm">
      <div class="mb-3">
        <label for="companyName" class="form-label">Company Name</label>
        <input type="text" class="form-control" id="companyName" v-model="companyName" name="companyName" maxlength="255"
          required>
      </div>
      <div class="mb-3">
        <label for="cnpj" class="form-label">CNPJ</label>
        <input type="text" class="form-control" id="cnpj" v-model="cnpj" name="cnpj" maxlength="14" required>
      </div>
      <div class="button">
        <button type="button" class="btn_primary" @click="submitForm">Register</button>
        <button type="button" class="btn_primary" @click="deleteCompany">Exclude</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      companyName: '',
      cnpj: ''
    };
  },
  methods: {
    submitForm() {
      const formData = {
        nome: this.companyName,
        cnpj: this.cnpj
      };

      // Verificar se a empresa já existe
      fetch('http://localhost:3000/empresas', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json'
        }
      })
        .then(response => {
          if (response.ok) {
            return response.json(); // Obter o corpo da resposta como JSON
          } else {
            throw new Error('Erro ao obter as empresas');
          }
        })
        .then(data => {
          // Verificar se a empresa já existe no array de empresas
          const existingCompany = data.find(company => company.nome === formData.nome && company.cnpj === formData.cnpj);
          if (existingCompany) {
            // A empresa já existe
            const companyId = existingCompany.id;
            alert('A empresa já está cadastrada.');
            this.companyName = '';
            this.cnpj = '';
            this.$router.push(`/empresa/${companyId}`); // Redirecionar para a rota dinâmica com o ID da empresa existente
          } else {
            // A empresa não existe, pode criar uma nova
            this.createCompany(formData);
          }
        })
        .catch(error => {
          console.error('Erro ao verificar se a empresa existe:', error);
          alert('Erro ao verificar se a empresa existe. Por favor, tente novamente.');
        });
    },
    createCompany(formData) {
      fetch('http://localhost:3000/empresas', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(formData)
      })
        .then(response => {
          if (response.ok) {
            return response.json(); // Obter o corpo da resposta como JSON
          } else {
            throw new Error('Erro ao cadastrar empresa');
          }
        })
        .then(data => {
          const newCompanyId = data.id; // Obter o ID da empresa criada
          alert('Empresa cadastrada com sucesso!');
          this.companyName = '';
          this.cnpj = '';
          this.$router.push(`/empresa/${newCompanyId}`); // Redirecionar para a rota dinâmica com o ID da empresa
        })
        .catch(error => {
          console.error('Erro ao cadastrar empresa:', error);
          alert('Erro ao cadastrar empresa. Por favor, tente novamente.');
        });
    },
    deleteCompany() {
      const formData = {
        nome: this.companyName,
        cnpj: this.cnpj
      };

      fetch('http://localhost:3000/empresas', {
        method: 'DELETE',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(formData)
      })
        .then(response => {
          if (response.ok) {
            // Empresa excluída com sucesso
            alert('Empresa excluída com sucesso!');
            this.companyName = '';
            this.cnpj = '';
          } else if (response.status === 404) {
            // Empresa não encontrada
            alert('Empresa não encontrada. Verifique o nome e o CNPJ informados.');
          } else {
            // Ocorreu um erro ao excluir a empresa
            alert('Erro ao excluir empresa. Por favor, tente novamente.');
          }
        })
        .catch(error => {
          console.error('Erro ao excluir empresa:', error);
          alert('Erro ao excluir empresa. Por favor, tente novamente.');
        });
    }
  }
};
</script>

<style scoped>
.form-label {
  color: #ccc;
  font-size: 18px;
  font-weight: 700;
}

.form_label {
  font-size: 30px;
  margin-bottom: 1rem;
  font-weight: 700;
  background: linear-gradient(to bottom, #fd5949, #285AEB);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.form_container {
  padding-top: 6rem;
  margin: auto;
  max-width: 50%;
  margin-bottom: 10rem;
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
