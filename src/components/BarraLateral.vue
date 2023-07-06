<template>
    <form>
        <h1>Lista de Tarefas</h1>

        <label for="titulo">Insira o título da tarefa:</label>
        <input type="text" id="titulo" v-model="titulo">

        <label for="descricao">Insira a descrição da tarefa:</label>
        <textarea type="text" id="descricao" v-model="descricao"></textarea>

        <label for="data">Insira o prazo da tarefa:</label>
        <input type="date" id="data" v-model="prazo">

        <button @click="salvarLocal">Incluir Tarefa</button>
    </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'BarraLateral',
    emits: ['aoSalvarTarefa'],
    data() {
        return {
            titulo: "",
            descricao: "",
            prazo: ""
        }
    },
    methods: {
        salvarLocal() {
            if (localStorage.cards) {
                var listaCards = JSON.parse(localStorage.getItem('cards') || '{}');
            } else {
                listaCards = [];
            }

            let prioridade = "";

            const dataAtual = new Date();
            const dataHoje: number = dataAtual.getDate();
            const mesAtual: number = dataAtual.getMonth() + 1;
            const anoAtual: number = dataAtual.getFullYear();

            const dataPrazo = Number(this.prazo.slice(8));
            const mesPrazo = Number(this.prazo.slice(5, 7));
            const anoPrazo = Number(this.prazo.slice(0, 4));

            if (anoPrazo > anoAtual) {
                prioridade = "Em tempo";
            } else if (anoPrazo === anoAtual) {
                if (mesPrazo > mesAtual) {
                    prioridade = "Em tempo";
                } else if (mesPrazo === mesAtual) {
                    if (dataPrazo - dataHoje <= 3) {
                        prioridade = "Urgentíssimo";
                    } else if (dataPrazo - dataHoje <= 6) {
                        prioridade = "Urgente";
                    } else if (dataPrazo - dataHoje <= 12) {
                        prioridade = "Moderado";
                    } else {
                        prioridade = "Em tempo";
                    }
                } else if (mesPrazo < mesAtual) {
                    alert("Mês informado é anterior ao mês vigente.");
                    prioridade = "Erro!";
                }
            } else if (anoPrazo < anoAtual) {
                alert("Ano informado é anterior ao ano vigente.");
                prioridade = "Erro!";
            }

            listaCards.push([this.titulo, this.descricao, this.prazo, listaCards.length + 1, prioridade]);
            localStorage.cards = JSON.stringify(listaCards);
        }
    }
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
    min-height: 100vh;
    width: 100%;

    h1 {
        margin: 3rem 0;
        font-size: 2.5rem;
    }

    label,
    input,
    textarea {
        width: 80%;
        font-size: 1.2rem;
    }

    input,
    textarea {
        border-radius: 8px;
        padding: 0.5rem;
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
