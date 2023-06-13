<template>
    <article class="card">
        <div>
            <h3 class="titulo-card">titulo</h3>
            <div>
                <button class="btn-edita">
                    <span class="material-symbols-outlined">edit</span>
                </button>
                <button class="btn-exclui">X</button>
            </div>
        </div>
        <p class="descricao-card">Descrição: descrição......</p>
        <div>
            <p class="prazo-card">Prazo: 12/12/2012</p>
            <p class="prioridade-card">Prioridade: Tranquila</p>
        </div>
        <button class="btn-realizada">Tarefa realizada<span class="material-symbols-outlined">check_circle</span></button>
    </article>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'CardTarefas'
})
</script>

<style scoped lang="scss">
    @import '../style/variaveis.scss';
    .card {
        border: 5px solid $cor-terciaria;
        background-color: $cor-primaria;
        border-radius: 20px;
        width: 25%;
        padding: 0 1rem 1rem 1rem;
        color: $cor-quaternaria;
        div {
            display: flex;
            justify-content: space-between;
            align-items: center;
            .titulo-card {
                font-size: 1.3rem;
                font-weight: 900;
            }
            .titulo-card + div {
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
                padding: 0.6rem;
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
        }
        .prazo-card,
        .prioridade-card {
            font-size: 0.8rem;
            width: 45%;
        }
        .btn-realizada {
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
</style>