<script setup>
let nomes = ['Alice', 'Bruna', 'Caio', 'Daniel', 'Ellen']
</script>

<template>
    <ul>
        //Diretiva geralemnte utilizada em listas ou tabelas
        <li v-for="pessoa in nomes">{{ pessoa }}</li>
    </ul>
</template>

/* Obs: Todas as vezes que criar um novo componente preciso importa-lo 
dentro de App.vue dentro da tag script e chama-lo dentro da tag tamplate, 
através do nome do import dado ao novo componente(nome qualquer) */ 