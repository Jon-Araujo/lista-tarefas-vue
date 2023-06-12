<template>
    <form>
        <h1>Lista de Tarefas</h1>

        <label for="titulo">Insira o título da tarefa:</label>
        <input type="text" id="titulo">

        <label for="descricao">Insira a descrição da tarefa:</label>
        <textarea type="text" id="descricao"></textarea>

        <label for="data">Insira o prazo da tarefa:</label>
        <input type="date" id="data">

        <button>Incluir Tarefa</button>
    </form>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    
    export default defineComponent({
        name: 'BarraLateral'
    })
</script>

<style scoped lang="scss">
    @import '../style/variaveis.scss';

    form {
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        background-color: $cor-terciaria;
        color: $cor-primaria;
        height: 100vh;
        h1 {
            margin: 3rem 0;
            font-size: 2.5rem;
        }
        label,
        input,
        textarea {
            width: 80%;
            font-size: 1.35rem;
        }
        input,
        textarea {
            border-radius: 8px;
            padding: 0.3rem;
            margin: 1rem 0 2rem;
            color: $cor-quaternaria;
        }
        button {
            padding: 0.8rem;
            font-size: 1.1rem;
            color: $cor-terciaria;
            background-color: $cor-primaria;
            border: none;
            border-radius: 8px;
        }
    }
</style>
