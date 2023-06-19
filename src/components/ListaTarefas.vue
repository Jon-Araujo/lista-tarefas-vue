<template>
    <section>
        <CardTarefas />
    </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CardTarefas from './CardTarefas.vue';

export default defineComponent({
    name: "ListaTarefas",
    components: {
        CardTarefas
    }
})
</script>

<style lang="scss" scoped>
    section {
        display: grid;
        grid-template-columns: 30% 30% 30%;
        gap: 5%;
        justify-content: space-between;
    }
</style>
