<!--
    PROPS -> Propriedades

    A utilização de Props fornece uma comunicação entre componentes, 
    enviar informeções Estáticas, Variáveis e Funções

-->

<!--SCRIPT-->

<script setup>
// Importanto componente

import Exemplo11Props2 from './Exemplo11Props2.vue';

// Variáveis
let cidade = "Teresina";

// Vetor
let estados = ['Maranhão', 'Piauí', 'Ceara', 'Pernambuco'];

//Função
function mensagem() {
    alert('Função criada no componente: Exemplo11Props1')
}

</script>

<!--HTML-->

<template>
    <!--Propriedade criada personalizada sem padrão obrigatório-->
    <!--Props dinamico por isso os pontos antes da PROPRIEDADE CIDADE-->

    <!--Variáveis e funções por serem dinanmicas exigem que na
        declaração em templates precisa haver os : antes do nome dado a 
        referencia 
    -->
    <!--Não existe importância para a ordem de declaração das propriedades -->

    <Exemplo11Props2 nome="Marlysson" idade="39" :cidade_v="cidade" :estados_v="estados" :funcao="mensagem">
    </Exemplo11Props2>
</template>

    