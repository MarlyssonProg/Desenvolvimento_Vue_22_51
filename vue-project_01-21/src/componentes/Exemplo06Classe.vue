<!--SCRIPT-->
<script setup>
// Variável
let validacao = true;
</script>
<!--CSS-->
<style>
.ok {
    color: green;
}

.falha {
    color: red;
}
</style>

<!--HTML-->
<template>
    <!--:class o mais atual -->
    <p :class="validacao ? 'ok' : 'falha'">Utilizando a diretiva class</p>
</template>

<!--Interligações de Classes-->