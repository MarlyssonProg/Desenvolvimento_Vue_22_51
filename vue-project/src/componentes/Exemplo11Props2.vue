<!--SCRIPT-->

<script setup>
// Obtendo props - Estático a partir do Exemplo11Props1.vue
// Sintaxe para receber propriedades estáticas a partir de uma const
// const props = defineProps(['nome', 'idade']);
let props = defineProps(['nome', 'idade', 'cidade_v', 'estados_v', 'funcao']);

</script>

<!--HTML-->

<template>
    <p>Nome: {{ nome }}</p>
    <p> Idade: {{ idade }}</p>
    <p> Cidade: {{ cidade }}</p>

    <ul>
        <li v-for="est of estados_v">{{ est }}</li>
    </ul>

    <button @click="funcao">Verificar</button>
</template>