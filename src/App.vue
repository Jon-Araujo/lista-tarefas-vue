<template>
  <aside>
    <BarraLateral />
  </aside>

  <main>
    <ListaTarefas />
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import ListaTarefas from './components/ListaTarefas.vue';

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    ListaTarefas
  }
});
</script>

<style lang="scss">
  @import './style/variaveis.scss';

  #app {
    background-color: $cor-secundaria;
    font-size: 16px;
    font-family: 'Maven Pro', sans-serif;
    display: flex;
    width: 100vw;
  }

  aside {
    width: 30%;
  }

  main {
    width: 70%;
    padding: 5% 10%;
  }
</style>
