<!--SCRIPT-->
<script setup>
//Função sem parâmetro
function mensagem() {
    alert('Executando a função evento de teclado!');
}
</script>

<!--HTML-->
<template>
    <!--O @keyup. é utilizado para chamar um evento de interação do teclado, onde pode-se utilizar-lo para validação do
    input e a tecla (@keyup.tecla) a qual foi chamado e digitado respectivamente-->
    <input type="text" @keyup.enter="mensagem">
</template>