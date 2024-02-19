<!--SCRIPT-->

<script setup>
// Importação do Bootstrap
import 'bootstrap/dist/css/bootstrap.min.css'

//Importação - VUE
import { onMounted, ref } from 'vue';

// Vetor reativo de produtos - atera-se sua visualização
let produtos = ref([]);

// Visisbilidade dos botões
let btnCadastrar = ref(true);

//Lifecycle -  OnMounted (Requisição do TIPO GET)
// Uso de um hook onMounted para executar a lógica quando o componente é montado.
onMounted(() => {
    // Fazendo uma requisição a um Endpoint que fornece dados de produtos da API
    fetch('http://localhost:3000/produtos')
        //Usando o método, .then para converter uma promise de resposta convertida em JSON
        .then(requisicao => requisicao.json())
        //Retorno da promisse de resposta convertida em arquivo json
        .then(retorno => produtos.value = retorno);

});

// Objeto do tipo produto
// Realizará o cadastro de produtos, onde a ID será medida pelo length acrescido mais 1 
// para haver uma geração sequencial de números únicos.
let obj = ref({ 'id': produtos.value.length + 1, 'produto': '', 'valor': 0 });

//Função Cadastro de produtos
function cadastrar(event) {

    if (produtos.value.length > 0) {
        obj.value.id = produtos.value[produtos.value.length - 1].id + 1;
    } else {
        obj.value.id = 1;
    }

    //Requisição POST
    fetch('http://localhost:3000/produtos', {
        //Especifica o tipo de requisição 
        //GET (Default - Padrão, sem necessidade de um segundo parametros),
        //POST,PUT,DELETE (Todos esses precisam do segundo método)
        method: 'POST',
        // Objeto a ser cadastrado = body
        // Conversão do objeto em texto json, para ser enviado pela requisição    
        body: JSON.stringify(obj.value),
        // Especificação tipo de dado manipulado (texto, JSON, XML etc)
        headers: { 'Content-Type': 'application/json' }
    })
        //Conversão da requisição em JSON
        .then(requisicao => requisicao.json())
        //Exibição do JSON convertido
        .then(retorno => {

            //Cadastrando novo produto no vetor
            produtos.value.push(retorno)

            //Limpando os inputs

            obj.value.produto = '';
            obj.value.valor = 0;

        });


    //PreventDefault 
    //Previne da página sofrer um refresh ao ser cadastrado! Porque não pode ser carregada?
    // Se utilizar P maiusculo do preventDefault como sugere a IDE, não funciona
    event.preventDefault();
}

//Function para selecionar um produto cadastrado 
function selecionarProduto(indice) {
    obj.value = {
        id: produtos.value[indice].id,
        produto: produtos.value[indice].produto,
        valor: produtos.value[indice].valor
    }
    btnCadastrar.value = false;
}

//Função Editar de produtos
function editarProdutos() {

    //Requisição POST
    fetch(`http://localhost:3000/produtos/${obj.value.id}`, {
        //Especifica o tipo de requisição 
        //GET (Default - Padrão, sem necessidade de um segundo parametros),
        //POST,PUT,DELETE (Todos esses precisam do segundo método)
        method: 'PUT',
        // Objeto a ser editado = body
        // Conversão do objeto em texto json, para ser enviado pela requisição    
        body: JSON.stringify(obj.value),
        // Especificação tipo de dado manipulado (texto, JSON, XML etc)
        headers: { 'Content-Type': 'application/json' }
    })
        //Conversão da requisição em JSON
        .then(requisicao => requisicao.json())
        //Exibição do JSON convertido
        .then(retorno => {

            // Obter o indice do vetor a qual desejo editar
            let indiceProduto = produtos.value.findIndex(objP => {
                return objP.id === retorno.id;
            });

            //Editar produto no vetor
            produtos.value[indiceProduto] = retorno;

            // Alterar a visibilidade dos botões
            btnCadastrar.value = true;

            //Limpando os inputs
            obj.value.id = 0;
            obj.value.produto = '';
            obj.value.valor = 0;

        });

}

//Função Remover de produtos
function removerProdutos() {

    //Requisição POST
    fetch(`http://localhost:3000/produtos/${obj.value.id}`, {
        //Especifica o tipo de requisição 
        //GET (Default - Padrão, sem necessidade de um segundo parametros),
        //POST,PUT,DELETE (Todos esses precisam do segundo método)
        method: 'DELETE',
        // Especificação tipo de dado manipulado (texto, JSON, XML etc)
        headers: { 'Content-Type': 'application/json' }
    })
        //Conversão da requisição em JSON
        .then(requisicao => requisicao.json())
        //Exibição do JSON convertido
        .then(() => {

            // Obter o indice do vetor a qual desejo editar
            let indiceProduto = produtos.value.findIndex(objP => {
                return objP.id === obj.value.id;
            });

            //Remover produto no vetor
            produtos.values.splice(indiceProduto, 1);

            // Alterar a visibilidade dos botões
            btnCadastrar.value = true;

            //Limpando os inputs
            obj.value.id = 0;
            obj.value.produto = '';
            obj.value.valor = 0;

        });

}


</script>

<!--CSS-->
<style>
form {
    width: 50%;
    margin: 30px auto;
    text-align: center;

}

input {
    margin-bottom: 10px;
}

.espacamentoBtn {
    margin-left: 5px;
    margin-right: 5px;
}
</style>
<!--HTML-->

<template>
    <!--FORMULÁRIO DE CADASTRO DE PRODUTOS-->
    <form @submit="cadastrar">
        <!--Teste para saber se estva funcionando o objeto do tipo produto criado no script-->
        <!-- <p>{{ obj }}</p> -->
        <input type="hidden" v-model="obj.id">
        <input type="text" placeholder="Produto" class="form-control" v-model="obj.produto">
        <input type="number" placeholder="Valor" class="form-control" v-model="obj.valor">
        <input type="submit" v-if="btnCadastrar" value="Cadastrar" class="btn btn-primary">
        <input type="button" @click="editarProdutos" v-if="!btnCadastrar" value="Editar"
            class="btn btn-primary espacamentoBtn">
        <input type="button" @click="removerProdutos" v-if="!btnCadastrar" value="Remover" class="btn btn-primary">

    </form>
    <!--TABELA-->
    <!--Classe Bootstrap que formata e colori linhas de uma tabela renderizada na template-->
    <table class="table table-striped">
        <thead>
            <tr>
                <th>ID</th>
                <th>Produto</th>
                <th>Valor</th>
                <th>Selecionar</th>
            </tr>
        </thead>

        <tbody>
            <tr v-for="(p, indice) in produtos">
                <td>{{ p.id }}</td>
                <td>{{ p.produto }}</td>
                <td>{{ p.valor }}</td>
                <td><button @click="selecionarProduto(indice)" class="btn btn-primary">Selecionado</button></td>
            </tr>
        </tbody>

    </table>
</template>
