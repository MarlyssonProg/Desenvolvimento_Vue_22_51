<script setup>
// Variável
let texto = '<p style="color:red">Aprendendo a diretiva v-html</p>';
</script>

<template>
    <!--Diferencia-se da interpolação de textos por conseguir reproduzir
        estruturas inteiras html, estilos e scripts-->
    <div v-html="texto"></div>

    <!--Não consegue converter a teg p em código, nem a configuração
        do CSS -->
    <div> {{ texto }}</div>
</template>