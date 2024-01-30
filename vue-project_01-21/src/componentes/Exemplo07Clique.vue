<!--SCRIPT-->

<script setup>
//Função 
function mensagem() {
    alert('Eventos de clique, AQUI!');
}
</script>

<!--HTML-->

<template>
    <!--Utiliza-se o @ para chamar eventos dentro da estrutura html-->
    <button @click="mensagem()">Clique aqui</button>
</template>
