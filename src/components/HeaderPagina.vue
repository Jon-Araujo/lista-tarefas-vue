<template>
    <header>
        <button @click="emitirAbreBarra">
            <span v-if="mostrarBarra == false" class="material-symbols-outlined">menu</span>
            <span v-else class="material-symbols-outlined">menu_open</span>
        </button>
        <div>
            <h1>Lista de Tarefas</h1>
            <h3>Gerencie de forma eficiente as tarefas diárias e garanta que nada seja esquecido ou negligenciado!</h3>
        </div>
    </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: "HeaderPagina",
    emits: ['abrirBarra'],
    data() {
        return {
            mostrarBarra: false
        }
    },
    methods: {
        emitirAbreBarra() {
            this.mostrarBarra = !this.mostrarBarra
            this.$emit('abrirBarra', this.mostrarBarra);
        }
    }
})
</script>

<style scoped lang="scss">
@import '../style/variaveis.scss';

header {
    background-color: $cor-quaternaria;
    padding: 1rem;
    display: flex;
    align-items: center;
    button {
        display: inline-block;
        padding: 1rem;
        background-color: $cor-primaria;
        border-radius: 20%;
        height: 70%;
    }

    div {
    text-align: center;
    width: 100%;
    display: inline-block;
        h1 {
            font-size: 2.5rem;
            color: $cor-primaria;
            margin: 0;
            width: 100%;
        }

        h3 {
            color: $cor-primaria;
            margin: 0.5rem 0 0 0;
        }
    }


}
</style>