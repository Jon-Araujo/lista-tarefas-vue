<template>
    <article class="card">
    <h3 class="titulo-card">titulo</h3>
    <button class="btn-exclui">X</button>
        <p class="descricao-card">Descrição: descrição......</p>
        <div>
            <p class="prazo-card">Prazo:............</p>
            <p class="prioridade-card">Prioridade: Tranquila</p>
        </div>
        <button class="btn-realizada">Tarefa realizada<span class="material-symbols-outlined">check_circle</span></button>
    </article>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
    name: 'ListaTarefas'
})
</script>

<style scoped lang="scss">
    @import '../style/variaveis.scss';
    .card {
        border: 5px solid $cor-terciaria;
        background-color: $cor-primaria;
        border-radius: 20px;
        width: 25%;
        padding: 1rem;
    }
</style>