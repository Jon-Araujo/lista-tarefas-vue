<template>
    <div @editaCard="verificaCard" class="conteudo">
        <div>
            <button @click="retorna"><span class="material-symbols-outlined">undo</span></button>
            <input type="text" id="titulo" v-model="titulo" :placeholder="titulo">
        </div>
        <form>
            <label for="descricao">Descrição:</label>
            <textarea type="text" id="descricao" v-model="descricao"></textarea>

            <label for="data">Prazo:</label>
            <input type="date" id="data" v-model="prazo">
            <button @click="confirmaEdicao">Confirmar</button>
        </form>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'EditaTarefa',
    emits: ['retornaEdicao'],
    data() {
        return {
            titulo: "",
            descricao: "",
            prazo: "",
            idCard: 0
        }
    },
    methods: {
        retorna() {
            this.$emit('retornaEdicao')
        },
        verificaCard(id: number, index: number) {
            let lista = JSON.parse(localStorage.getItem('cards') || '{}')
            alert(id);
            alert(index)

            this.idCard = id;

            this.titulo = lista[index][0];
            this.descricao = lista[index][1];
            this.prazo = lista[index][2]
        },
        confirmaEdicao() {
            console.log("confirma edição");
        }

    }
})
</script>

<style lang="scss" scoped>
@import '../style/variaveis.scss';

.conteudo {
    display: flex;
    flex-direction: column;
    height: 100%;
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
            padding: 0.3rem
        }
    }

    form {
        #descricao {
            width: 100%;
            margin: 0.5rem 0;
            height: 45%;
            padding: 0.3rem
        }

        #data {
            margin-left: 0.3rem;
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