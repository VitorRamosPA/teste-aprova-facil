<template>
    <div class="inv" id="disc">
        <p>Preencha corretamente abaixo</p>
        <div>
            <form id="cadastro-form" @submit="createCadastro" @submit.prevent="submitForm">
                <div class="input-container">
                    <label for="nome">Nome Completo:</label>
                    <input type="text" id="nome" name="name" v-model="nome" placeholder="Ex - Fulano José da Rosa">
                </div>
                <div class="input-container">
                    <label for="cpf">CPF:</label>
                    <input type="text" id="cpf" name="cpf" v-model="cpf" placeholder="Ex - 999.999.999-25">
                </div>
                <div class="input-container">
                    <label for="rg">RG:</label>
                    <input type="text" id="rg" name="rg" v-model="rg" placeholder="Ex - 99.999.999-9">
                </div>
                <div class="input-container">
                    <label for="nascimento">Data de Nascimento:</label>
                    <input type="text" id="nascimento" name="nascimento" v-model="data_nasc" placeholder="Ex - 01/01/2001">
                </div>
                <div class="input-container">
                    <label for="sexo">Sexo:</label>
                    <select name="sexo" id="sexo" v-model="sexo" >
                        <option value="masculino"> Masculino </option>
                        <option value="feminino"> Feminino </option>
                    </select>
                </div>
                <div  class="input-container btn btn-white">
                    <input type="submit" class="submit-btn" value="Criar Pessoa">
                </div>
                <Message :msg="msg" v-show="msg"/>
            </form>
        </div>
    </div>
</template>
<script>
import Message from '../components/Message.vue';
export default {
  components: { Message },
    
    name: "Form",
    data() {
        return {
            nome: null,
            cpf: null,
            rg: null,
            data_nasc: null,
            sexo: null,
            msg: null
        }
    },
    methods: {
        async createCadastro(e) {
            e.preventDefault();

            const data = {
                nome: this.nome,
                cpf: this.cpf,
                rg: this.rg,
                data_nasc: this.data_nasc,
                sexo: this.sexo
            }

            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/pessoas", {
                method: "POST",
                headers: { "Content-Type": "application/json"},
                body: dataJson
            });
            

            const res = await req.json();

            this.msg = `Cadastro de ${res.nome} realizado com sucesso`;

            this.nome = "";
            this.cpf = "";
            this.rg = "";
            this.data_nasc = "";
            this.sexo = "";
        },
        async processaTeste(e){
            console.log(e);
        }
        
    },
    mounted () {
        this.$root.$on('editarPessoa', pessoa => {
            console.log(pessoa);
        })
    }
}
</script>

<style scoped>
.btn:hover {
    transform: translateY(-3px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.btn:active {
    transform: translateY(-1px);
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

.btn-white {
    background-color: #fff;
    color: #777;
    padding: 1px; 
    width: 100px;
    margin-left: auto;
    border: 1px solid rgb(33, 33, 253);
    border-radius: 25px;
    align-items: center;

}
#disc {
    margin-top: 70px;
}

 #cadastro-form {
    width: 400px;
    margin: 0 auto;
 }

 .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
 }

 label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid rgb(16, 32, 255);
 }

</style>