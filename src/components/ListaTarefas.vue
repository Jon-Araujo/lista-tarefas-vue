<template>
    <section>
        <CardTarefas v-for="(card, index) in cards" :key="index" :card="card"/>
    </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CardTarefas from './CardTarefas.vue';

export default defineComponent({
    name: "ListaTarefas",
    components: {
        CardTarefas
    },
    data() {
        return {
            cards: []
        }
    },
    methods: {
        
    }
})
</script>
