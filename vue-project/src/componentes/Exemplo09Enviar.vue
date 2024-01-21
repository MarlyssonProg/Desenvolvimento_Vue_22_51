<!--SCRIPT-->
<script setup>
// Função de validação do formulário
function validaFormulario() {
    alert('Formulario enviado com sucesso!')
}

</script>

<!--HTML-->
<template>
    <form @submit="validaFormulario">
        <input type="submit" value="Enviar formulário">

    </form>
</template>