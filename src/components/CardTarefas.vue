<template>
    <article class="card" v-for="(card, index) in cards" :key="index" :card="card">
        <span v-if="contadorId !== card[3]">
            <div>
                <h3 v-if="card[5] === 'realizada'" class="titulo-card" :style="`text-decoration: ${textDecorationStyle}`">{{
                    card[0] }}</h3>
                <h3 v-else class="titulo-card">{{ card[0] }}</h3>
                <div>
                    <button class="btn-edita" @click="editarTarefa(card[3], index)">
                        <span class="material-symbols-outlined">edit</span>
                    </button>
                    <button class="btn-exclui" @click="excluirTarefa(index)"><span
                            class="material-symbols-outlined">close</span></button>
                </div>
            </div>
            <p v-if="card[5] === 'realizada'" class="descricao-card" :style="`text-decoration: ${textDecorationStyle}`">
                Descrição: {{ card[1] }}</p>
            <p v-else class="descricao-card">Descrição: {{ card[1] }}</p>
            <div v-if="card[5] === 'realizada'">
                <p class="prazo-card" :style="`text-decoration: ${textDecorationStyle}`">Prazo: {{ card[2] }}</p>
                <p class="prioridade-card" :style="`text-decoration: ${textDecorationStyle}`">Prioridade: {{ card[4] }}</p>
            </div>
            <div v-else>
                <p class="prazo-card">Prazo: {{ card[2] }}</p>
                <p class="prioridade-card">Prioridade: {{ card[4] }}</p>
            </div>
            <button v-if="card[5] === 'realizada'" class="btn-realizada" @click="concluirTarefa(index)"
                :style="`background-color: ${bgColor}`">Tarefa realizada<span
                    class="material-symbols-outlined">check_circle</span></button>
            <button v-else class="btn-realizada" @click="concluirTarefa(index)">Tarefa realizada<span
                    class="material-symbols-outlined">check_circle</span></button>
        </span>

        <span v-else>
            <EditaTarefa @retornaEdicao="contadorId = 0"
                v-bind="{ id: card[3], index: index, tituloCard: card[0], descricaoCard: card[1], prazoCard: card[2] }" />
        </span>
    </article>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import EditaTarefa from './EditaTarefa.vue'

export default defineComponent({
    name: 'CardTarefas',
    components: {
        EditaTarefa
    },
    data() {
        return {
            cards: JSON.parse(localStorage.getItem('cards') || '{}'),
            textDecorationStyle: "line-through",
            bgColor: "#00A000;",
            contadorId: 0
        }
    },
    methods: {
        excluirTarefa(index: number) {
            this.cards.splice(index, 1);
            localStorage.cards = JSON.stringify(this.cards);
        },

        editarTarefa(id: number, index: number) {
            this.contadorId = id;
        },

        concluirTarefa(index: number) {
            const lista = JSON.parse(localStorage.cards)
            if (lista[index].length === 5) {
                this.cards[index].push("realizada");
            } else if (lista[index].length === 6) {
                this.cards[index].pop();
            }
            localStorage.cards = JSON.stringify(this.cards);
        }
    }
})
</script>

<style scoped lang="scss">
@import '../style/variaveis.scss';

.card {
    border: 5px solid $cor-terciaria;
    background-color: $cor-primaria;
    border-radius: 20px;
    width: auto;
    padding: 0 1rem 1rem 1rem;
    color: $cor-quaternaria;
    height: auto;
    margin-top: 15%;
    display: flex;
    flex-direction: column;

    span {
        height: 100%;

        div {
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-height: 20%;
            margin-top: 0.5rem;

            .titulo-card {
                font-size: 1.3rem;
                font-weight: 900;
            }

            .titulo-card+div {
                height: 2rem;

                .btn-edita {
                    border-radius: 40%;
                    max-height: 100%;
                    width: 45%;
                    padding: 0.6rem;
                    color: $cor-primaria;
                    background-color: $cor-quaternaria;
                    border: none;
                    transition: 0.5s;
                    display: flex;
                    align-items: center;
                    justify-content: center;

                    &:hover {
                        transition: 0.5s;
                        transform: scale(1.1);
                        background-color: #F3D500;
                        color: $cor-quaternaria;
                    }
                }

                .btn-exclui {
                    border-radius: 40%;
                    height: 100%;
                    width: 45%;
                    padding: 0.3rem;
                    color: $cor-primaria;
                    background-color: $cor-quaternaria;
                    border: none;
                    transition: 0.5s;

                    &:hover {
                        transition: 0.5s;
                        transform: scale(1.1);
                        background-color: #FF0000;
                    }
                }
            }
        }

        .descricao-card {
            font-size: 1.1rem;
            height: 30%;
        }

        .prazo-card {
            width: 70%;
            font-size: 0.8rem;
        }

        .prioridade-card {
            width: 30%;
            font-size: 0.8rem;
        }

        .btn-realizada {
            margin: 0.5rem 0 2rem 0;
            display: flex;
            align-items: center;
            width: 100%;
            justify-content: space-around;
            transition: 0.5s;
            border: none;
            border-radius: 8px;
            padding: 0.4rem;
            color: $cor-primaria;
            background-color: $cor-quaternaria;
            font-weight: 700;

            &:hover {
                background-color: #00A000;
                transition: 0.5s;
            }
        }
    }
}</style>