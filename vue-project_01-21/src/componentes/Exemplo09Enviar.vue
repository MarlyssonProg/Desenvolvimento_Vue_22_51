<!--SCRIPT-->
<script setup>
// Função de validação do formulário
function validaFormulario(event) {   // Redirecionamento impedido ao adicionar o event dentro do parenteses
    alert('Formulario enviado com sucesso!')

    event.preventDefault();          //  E adição desta linha nessa sintaxe 
}

</script>

<!--HTML-->
<template>
    <!--form com o atributo action, que faz o redirecionamento do usuário após o alert da 
        function validaFormulario para meu git hub-->
    <form action="https://github.com/MarlyssonProg" @submit="validaFormulario">
        <input type="submit" value="Enviar formulário">

    </form>
</template>

<!--OBS: Ao fazer um clone localmente na minha máquina do meu repoisitório do meu GitHub
         Tive dificuldade para iniciar o servidor com o comando NPM RUN DEV, porém ao 
         reinstalar o vite, pelo próprio terminal com o comando NPM INSTALL VITE
         tudo voltou a funcionar conforme o previsto
        
        O preventDegfault então pode ser utilizado em formulário que não permitirar o redirecionamento, 
        todos os campos dos formularios não estiverem devidamente preenchidos -->