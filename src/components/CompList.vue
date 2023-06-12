<template>
    <div class="list_title">
      Registered <div class="colored">Companies:</div> 
    </div>
    <div class="list_container">
      <div class="table_state">
        <table>
          <thead>
            <tr>
              <th class="table_head" scope="col">Nome</th>
              <th scope="col">CNPJ</th>
            </tr>
          </thead>
          <tbody>
            <tr class="table_body" v-for="(empresa, index) in empresas" :key="empresa.id">
              <td class="">{{ empresa.nome }}</td>
              <td>
                {{ empresa.cnpj }} 
                <router-link :to="'/address/' + empresa.id" class="btn_adress">Address</router-link>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  
  
<script>
export default {
    data() {
        return {
            empresas: []
        };
    },
    mounted() {
        this.fetchEmpresas();
    },
    methods: {
        async fetchEmpresas() {
            try {
                const response = await fetch('http://localhost:3000/empresas');
                if (response.ok) {
                    this.empresas = await response.json();
                } else {
                    console.error('Erro ao obter as empresas:', response.statusText);
                    console.error('Detalhes do erro:', await response.text());
                }
            } catch (error) {
                console.error('Erro ao conectar com o servidor:', error);
            }
        }
    }
};
</script>
  
<style scoped>
.list_title{
    margin-left: 12rem;
    display: flex;
    font-size: 30px;
    padding: 1rem;
    font-weight: 700;
    color: #ccc;
}
.colored{
    margin-left: .5rem;
    background: linear-gradient(to bottom, #fd5949, #285AEB);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.list_container {
    display: flex;
    justify-content: center;
    align-items: center;
    color: #ccc;
    min-width: 1200px;
}

table {
    width: 80%;
}

thead {
    font-size: 19px;
    padding-top: 2rem;
}

td {
    padding-top: 1rem;
    padding-bottom: 1rem;
    padding-left: .3rem;
}

.table_state {
    margin-top: 4rem;
    margin-bottom: 5rem;
    min-width: 1000px;
    margin: auto;
    display: flex;
    justify-content: center;
}

.table_head {
    padding-top: 1rem;
    padding-bottom: 1rem;
    width: 50%
}
.table_body:hover {
    background-color: #cfcfcf;
    color: black;
}

.btn_adress {
    margin-left: 9rem;
    background: linear-gradient(to bottom, #fd5949, #285AEB);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    font-weight: 600;
    color: #fff;
    box-shadow: none;
    transition: .2s ease;
    border: 1px solid;
    border-image: linear-gradient(to bottom, #fd5949, #285AEB) 1;
    border-image-slice: 1;
    border-radius: 8px;
    padding: .3rem;
}
.btn_adress:hover{
    filter: brightness(75%);
}

@media (max-width: 768px) {
  .list_container {
    min-width: auto;
  }

  table {
    width: 100%;
  }

  .list_title {
    margin-left: 1rem;
    font-size: 24px;
  }

  .table_state {
    margin-top: 2rem;
    margin-bottom: 3rem;
    min-width: auto;
  }

  .table_head {
    width: 60%;
  }

  .btn_adress {
    margin-left: 0;
  }
}
</style>