<!--SCRIPT-->

<script setup>
// Importação do Bootstrap
import 'bootstrap/dist/css/bootstrap.min.css'

//Importação - VUE
import { onMounted, ref } from 'vue';

// Vetor reativo de produtos - atera-se sua visualização
let produtos = ref([]);

//Lifecycle -  OnMounted 
// Uso de um hook onMounted para executar a lógica quando o componente é montado.
onMounted(() => {
    // Fazendo uma requisição a um Endpoint que fornece dados de produtos da API
    fetch('http://localhost:3000/produtos')
        //Usando o método, .then para converter uma promise de resposta convertida em JSON
        .then(requisicao => requisicao.json())
        //Retorno da promisse de resposta convertida em arquivo json
        .then(retorno => produtos.value = retorno);

});


</script>

<!--HTML-->

<template>
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
