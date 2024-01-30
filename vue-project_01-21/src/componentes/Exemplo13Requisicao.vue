<!--SCRIPT-->
<script setup>

//Importação
import { onMounted, ref } from 'vue';
// Variavel reativa - Contendo as postagens
let vetor = ref([]);

// Depois do componente montado acontecerá os passos abaixo
onMounted(() => {
    //Url da api falsa
    fetch('https://jsonplaceholder.typicode.com/posts')
        // Conversão do retorno de uma requisição a uma API, sendo convertida para JSON 
        .then(retorno_req => retorno_req.json())
        // Retorno da Requisição já em JSON, sendo armazenado na variável reativa vetor
        .then(retorno_conv => vetor.value = retorno_conv)
});

</script>

<!--HTML-->

<template>
    <h1>Requisições</h1>

    <table>
        <tr v-for="v in vetor">
            <td>{{ v.userId }}</td>
            <td>{{ v.id }}</td>
            <td>{{ v.title }}</td>
            <td>{{ v.body }}</td>
        </tr>
    </table>
</template>

