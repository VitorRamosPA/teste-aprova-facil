<template>
    <div class="main-container">
        <div class="content">
            <h1>Gerenciar Cadastros</h1>
            <div id="people-table">
                <div>
                    <div id="heading-table">
                    <div class="guy-id">Nº cadastros</div>
                    <div>Nome</div>
                    <div>CPF</div>
                    <div>RG</div>
                    <div>Nascimento</div>
                    <div>Sexo</div>
                    <div>Pessoas Cadastradas</div>
                </div>
            </div>
            <div id="table-rows">
                <div class="guy-table-row" v-for="pessoa in pessoas" :key="pessoa.id">
                    <div class="order-number">{{pessoa.id}}</div>
                    <div>{{pessoa.nome}}</div>
                    <div>{{pessoa.cpf}}</div>
                    <div>{{pessoa.rg}}</div>
                    <div>{{pessoa.data_nasc}}</div>
                    <div>{{pessoa.sexo}}</div>
                    <div>
                    <button class="delete-btn" @click="deletePessoa(pessoa.id)">Excluir</button>
                    <button class="edit-btn" @click="editaPessoa(pessoa)">Editar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import TableForm from '../components/TabledForm.vue'
export default {
    name: 'Cadastros',
    data() {
        return {
            pessoas: null,
            pessoas_id: null,            
        }
    },
    methods: {
        async getPessoas() {
            const req = await fetch("http://localhost:3000/Pessoas")

            const data = await req.json();

            this.pessoas = data;
        },
        async deletePessoa(id) {
            
            const req = await fetch(`http://localhost:3000/Pessoas/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            this.getPessoas();
        }, 
        async editaPessoa(pessoa){
            this.$root.$emit('editarPessoa', pessoa)
        }

},
    mounted() {
        this.getPessoas();
    },
    component: {
        TableForm,

    }
}
</script>

<style  scoped>
#table-rows {
    overflow: scroll;
    height: 600px;
}

#people-table {
    max-width: 1200px;
    margin: 0 auto;
}

#heading-table, #table-rows, .guy-table-row {
    display: flex;
    flex-wrap: wrap;
}

#heading-table {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}

#heading-table div, .guy-table-row div{
    width: 15%;
}

.guy-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc;
}

#heading-table .guy-id, .guy-table-row .order-number{
    width: 8%;
}
.guy-table-row .order-number {
    margin-left: 15px;
}

.delete-btn, .edit-btn {
    background-color: #333;
    color: whitesmoke;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
    transition: .5s;
    border-radius: 5px;
}

.delete-btn:hover, .edit-btn:hover{
    background-color: transparent;
    color: black;
}

.main-container {
    margin-top: 300px;
    z-index: 99;
    background-color: rgba(0, 0, 0, 0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid black;
    border-radius: 25px;

}

.content {
    background: #fff;
    padding: 100px;
    height: 700px;
    width: 1200px;
}

</style>