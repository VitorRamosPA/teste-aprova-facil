<template>
  <div class="main-div">
    <div class="input-container">
        <label for="nome">Filtrar por Nome</label>
        <input type="text" id="nome" name="name" v-model="nome" placeholder="Ex - Fulano José da Rosa">
        <div  class="input-container btn btn-white">
            <button class="search-btn" @click="getPessoasCPF(pessoa.nome)">Pesquisar Nome </button>
        </div>
        <label for="cpf">Filtrar por CPF</label>
        <input type="text" id="cpf" name="cpf" v-model="cpf" placeholder="999.999.999-99">
        <div  class="input-container btn btn-white">
            <input type="submit" class="search-btn" value="Pesquisar CPF">
        </div>
        <div id="table-rows">
            <div class="guy-table-row" v-for="pessoa in pessoas" :key="pessoa.id">
                <div class="order-number">{{pessoa.id}}</div>
                <div>{{pessoa.nome}}</div>
                <div>{{pessoa.cpf}}</div>
                <div>{{pessoa.rg}}</div>
                <div>{{pessoa.data_nasc}}</div>
                <div>{{pessoa.sexo}}</div>
            </div>
            </div>
        </div>    
  </div>
</template>

<script>
import TableForm from '../components/TabledForm.vue'

export default {
name: 'FilterData',
data() {
    return {
        pessoas: null,
        pessoas_id: null,            
    }
},
methods: {
    async getPessoasCPF(cpf) {
    const req = await fetch(`http://localhost:3000/Pessoas${cpf}`)

    const data = await req.json();

    this.pessoas = data;
    },
},
component:{
    TableForm
}

}
</script>

<style scoped>
.main-div{
    background-color: rgb(255, 249, 241);
}
.input-container {
    display: flex;
}

</style>