<template>
    <div class="adress_container">
        <router-link to="/companieslist" class="btn_adress">Return</router-link>
        <div class="adress_title">Adress <div class="colored"> Details</div>
        </div>
        <ul v-if="endereco">
            <li class="desc">
                {{ endereco.rua }}, {{ endereco.cidade }}, {{ endereco.estado }}, {{ endereco.cep }}
            </li>
        </ul>
        <p v-else class="desc">No address registered.</p>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            endereco: null
        };
    },
    mounted() {
        const empresaId = this.$route.params.empresa_id;
        this.fetchEndereco(empresaId);
    }
    ,
    methods: {
        async fetchEndereco(empresaId) {
            try {
                const response = await fetch(`http://localhost:3000/enderecos/${empresaId}`);
                if (response.ok) {
                    const data = await response.json();
                    this.endereco = data[0];
                } else {
                    console.error('Erro ao obter o endereço:', response.statusText);
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
.adress_container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    color: #ccc;
    margin-bottom: 19rem;
}

.adress_title {
    padding-top: 2rem;
    display: flex;
    font-weight: 700;
    font-size: 36px;
    padding-bottom: 2rem;
}
.desc{
    font-weight: 600;
    font-size: 22px;
}
.colored {
    margin-left: .5rem;
    background: linear-gradient(to bottom, #fd5949, #285AEB);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    margin-bottom: 0.5rem;
}

.btn_adress {
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
    align-self: flex-end;
    margin-right: 4rem;
    margin-top: 2rem;
    margin-bottom: 2rem;
}

.btn_adress:hover {
    filter: brightness(75%);
}
</style>
  