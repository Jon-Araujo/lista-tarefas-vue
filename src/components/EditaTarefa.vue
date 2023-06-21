<template>
    <div @editarTarefa="editandoCard" v-if="editandoCard">
        <div class="conteudo">
            <h2>Teste de edição de card</h2>
            <button @click="cancelaEdicao">Fechar</button>
            <p>Conteúdo a ser editado do card...</p>
            <button @click="confirmaEdicao">Confirmar</button>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'EditaTarefa',
    data() {
        return {
            editandoCard: false
        }
    },
    methods: {
        editaCard(editandoCard: boolean) {
            this.editandoCard = editandoCard;
        },
        cancelaEdicao() {
            console.log("cancela edição");
            // this.editandoCard = !this.editandoCard;
        },
        confirmaEdicao() {
            console.log("confirma edição");
        }

    }
})
</script>

<style lang="scss" scoped>
div {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;

    .conteudo {
        background-color: white;
        padding: 20px;
    }
}
</style>