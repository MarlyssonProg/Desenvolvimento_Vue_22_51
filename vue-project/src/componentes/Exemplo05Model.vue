<script setup>
/* Importando o REF - precisa ser importado, antes da declaração da 
variável a qual irá utiliza-lo */
import { ref } from 'vue';
// Variável
/* Obs: O comando ref antes do parênteses é responsável por transformar
transformar o input de texto em reativo, o que for digitado ser visto
na tag <p> (faz a ligação de javascript para html e html para java script*/
let texto = ref('');
</script>

<template>
    <!--Input utilizando a diretiva v-model-->
    <input type="text" v-model="texto">
    <!--Párágrafo onde aparecerá o que for digitado no input acima-->
    <p>{{ texto }}</p>
</template>

<!--DÚVIDAS-->
<!--É uma boa prática utilizar as chaves na importação do ref? Porque testei e ao tirar a mesma roda perfeitamente-->