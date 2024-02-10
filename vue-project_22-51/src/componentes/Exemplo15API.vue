<!--SCRIPT-->

<script setup>
//Importação - VUE
import { onMounted, ref } from 'vue';

// Vetor reativo de produtos - atera-se sua visualização
let produtos = ref([])

//Lifecycle -  OnMounted 
// Uso de um hook onMounted para executar a lógica quando o componente é montado.
onMounted(() => {
    // Fazendo uma requisição a um Endpoint que fornece dados de produtos da API
    fetch('http://localhost:3000/produtos')
        //Usando o método, .then para converter uma promise de resposta convertida em JSON
        .then(requisicao => requisicao.json)
        //Retorno da promisse de resposta convertida em arquivo json
        .then(retorno => produtos.value = retorno);

});


</script>

<!--HTML-->

<template>
    <!--TABELA-->
    <table>
        <thead>
            <tr>
                <th>Produto</th>
                <th>Valor</th>
                <th>Seleção</th>
            </tr>
        </thead>

        <tbody>
            <tr v-for="p in produtos">
                <td>{{ p.produto }}</td>
                <td>{{ p.valor }}</td>
                <td><button>Seleção</button></td>
            </tr>
        </tbody>
    </table>
</template>
