<!--SCRIPT-->

<script setup>
// Importação do Bootstrap
import 'bootstrap/dist/css/bootstrap.min.css'

//Importação - VUE
import { onMounted, ref } from 'vue';

// Vetor reativo de produtos - atera-se sua visualização
let produtos = ref([]);

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
// Realizará o cadastro de produtos
let obj = ref({ 'id': 0, 'produto': '', 'valor': 0 });

//Função de Cadastro de produtos
function cadastrar(event) {
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
</style>
<!--HTML-->

<template>
    <!--FORMULÁRIO DE CADASTRO DE PRODUTOS-->
    <form @submit="cadastrar">
        <!--Teste para saber se estva funcionando o objeto do tipo produto criado no script-->
        <!-- <p>{{ obj }}</p> -->
        <input type="text" placeholder="Produto" class="form-control" v-model="obj.produto">
        <input type="number" placeholder="Valor" class="form-control" v-model="obj.valor">
        <input type="submit" value="Cadastrar" class="btn btn-primary">
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
            <tr v-for="p in produtos">
                <td>{{ p.id }}</td>
                <td>{{ p.produto }}</td>
                <td>{{ p.valor }}</td>
                <td><button class="btn btn-primary">Selecionado</button></td>
            </tr>
        </tbody>

    </table>
</template>
