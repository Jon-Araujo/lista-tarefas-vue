<template>
    <div class="conteudo">
        <div>
            <button @click="retorna"><span class="material-symbols-outlined">undo</span></button>
            <input type="text" id="titulo" v-model="titulo" :placeholder="tituloCard">
        </div>
        <form>
            <label for="descricao">Descrição:</label>
            <textarea type="text" id="descricao" v-model="descricao" :placeholder="descricaoCard"></textarea>

            <label for="data">Prazo:</label>
            <input type="date" id="data" v-model="prazo" :placeholder="prazoCard">
            <button @click="confirmaEdicao(index)">Confirmar</button>
        </form>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'EditaTarefa',
    emits: ['retornaEdicao'],
    props: {
        id: Number,
        index: Number,
        tituloCard: String,
        descricaoCard: String,
        prazoCard: String
    },
    data() {
        return {
            titulo: "",
            descricao: "",
            prazo: "",
            prioridade: ""
        }
    },
    methods: {
        retorna() {
            this.$emit('retornaEdicao');
        },
        confirmaEdicao(i: number) {
            let lista = JSON.parse(localStorage.getItem('cards') || '{}');
            if (this.titulo == "") {
                this.titulo = lista[i][0];
            }
            if (this.descricao == "") {
                this.descricao = lista[i][1];
            }
            if (this.prazo == "") {
                this.prazo = lista[i][2];
            } else {
                const dataAtual = new Date();
                const dataHoje: number = dataAtual.getDate();
                const mesAtual: number = dataAtual.getMonth() + 1;
                const anoAtual: number = dataAtual.getFullYear();

                const dataPrazo = Number(this.prazo.slice(8));
                const mesPrazo = Number(this.prazo.slice(5, 7));
                const anoPrazo = Number(this.prazo.slice(0, 4));

                if (anoPrazo > anoAtual) {
                    this.prioridade = "Em tempo";
                } else if (anoPrazo === anoAtual) {
                    if (mesPrazo > mesAtual) {
                        this.prioridade = "Em tempo";
                    } else if (mesPrazo === mesAtual) {
                        if (dataPrazo - dataHoje <= 3) {
                            this.prioridade = "Urgentíssimo";
                        } else if (dataPrazo - dataHoje <= 6) {
                            this.prioridade = "Urgente";
                        } else if (dataPrazo - dataHoje <= 12) {
                            this.prioridade = "Moderado";
                        } else {
                            this.prioridade = "Em tempo";
                        }
                    } else if (mesPrazo < mesAtual) {
                        alert("Mês informado é anterior ao mês vigente.");
                        this.prioridade = "Erro!";
                    }
                } else if (anoPrazo < anoAtual) {
                    alert("Ano informado é anterior ao ano vigente.");
                    this.prioridade = "Erro!";
                }
            }
            lista[i][0] = this.titulo;
            lista[i][1] = this.descricao;
            lista[i][2] = this.prazo;
            lista[i][4] = this.prioridade;
            localStorage.cards = JSON.stringify(lista);
        }

    }
})
</script>

<style lang="scss" scoped>
@import '../style/variaveis.scss';

.conteudo {
    display: flex;
    flex-direction: column;
    height: auto;
    justify-content: space-between;

    div {
        display: flex;
        align-items: center;
        width: 100%;
        justify-content: space-between;
        padding: 0.5rem 0.5rem 1rem;

        button {
            border-radius: 40%;
            width: 15%;
            padding: 0.3rem 0.3rem 0.1rem 0.3rem;
            color: $cor-primaria;
            background-color: $cor-quaternaria;
            border: none;
            transition: 0.5s;
            margin: 0;

            &:hover {
                transition: 0.5s;
                transform: scale(1.1);
                background-color: $cor-primaria;
                color: $cor-quaternaria;
                border: 1px solid $cor-quaternaria;
            }
        }

        #titulo {
            padding: 0.2rem;
            margin-left: 0.3rem;
            width: 100%;
            border: 1px solid $cor-secundaria;
            border-radius: 8px;
            background-color: $cor-primaria;

            &::placeholder {
                font-size: 1.1rem;
                color: $cor-quaternaria;
            }
        }
    }

    form {
        height: 100%;

        #descricao {
            width: 95%;
            margin: 0.5rem 0;
            padding: 0.2rem;
            font-size: 0.9rem;
            height: 7rem;
            border: 1px solid $cor-secundaria;
            border-radius: 8px;
            background-color: $cor-primaria;

            &::placeholder {
                color: $cor-quaternaria;
            }
        }

        #data {
            margin-left: 0.3rem;
            color: $cor-quaternaria;
            padding: 0.2rem;
            margin-left: 0.3rem;
            border: 1px solid $cor-secundaria;
            border-radius: 8px;
            background-color: $cor-primaria;
        }

        button {
            width: 100%;
            transition: 0.5s;
            border: none;
            border-radius: 8px;
            padding: 0.6rem;
            margin-top: 0.5rem;
            color: #DDE6ED;
            background-color: #27374D;
            font-weight: 700;

            &:hover {
                transform: scale(1.1);
                background-color: #F3D500;
                color: $cor-quaternaria;
            }
        }
    }
}
</style>