<!--LifeCycle: Acões que podem acontecer 
             
               Antes || Durante || Depois da criação do componentes
               Dúvida - O LifeCycle geralmente ocorre um por vez ou em mais de um ou em quem sabe
               todos os momentos? Antes && Durante && Depois? -->


<!--SCRIPT-->
<script setup>
//Importações
                    // Obrigatoria importação do onMounted
    import { ref, onMounted } from 'vue';

//Variável de texto - VARIÁVEL REATIVA
    let texto = ref('Alterando em...!')

//LifeCycle onMounted - sintaxe
    onMounted(() => {
    setTimeout(() => {
        texto.value = 'Tchanraaaan!';

    }, 3000);
});

</script>

<!--HTML-->
<template>
    <!--Interpolação de texto-->
    <h1>{{ texto }}</h1>
</template>
               