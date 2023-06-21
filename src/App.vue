<template>
  <HeaderPagina @abrirBarra="abrirBarra" />

  <div class="principal">
    <aside v-if="mostrarBarra !== true" :style="`display: ${displayNone}`" >
      <BarraLateral />
    </aside>
    <aside v-else :style="`display: ${displayFlex}`" >
      <BarraLateral />
    </aside>

    <main>
      <ListaTarefas />
    </main>
  </div>

  <footer>
    <h3>Projeto de certificação mundo 2 - DevTeam xx</h3>
  </footer>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import ListaTarefas from './components/ListaTarefas.vue';
import HeaderPagina from './components/HeaderPagina.vue';

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    ListaTarefas,
    HeaderPagina
  },
  data() {
    return {
      mostrarBarra: false,
      displayFlex: "flex",
      displayNone: "none"
    }
  },
  methods: {
    abrirBarra(mostrarBarra: boolean) {
      this.mostrarBarra = mostrarBarra;
    }
  }
});
</script>

<style lang="scss">
@import './style/variaveis.scss';

html {
  min-height: 100vh;
}

body {
  margin: 0;
  height: auto;
}

#app {
  background-color: $cor-secundaria;
  font-size: 16px;
  font-family: 'Maven Pro', sans-serif;
  min-height: 100vh;
  height: auto;
}

.principal {
display: flex;
  aside {
    width: 40%;
  }

  main {
    width: 100%;
    padding: 2% 5%;
    min-height: 100vh;
  }
}



footer {
  position: relative;
  bottom: 0;
  padding: 0.1rem;
  text-align: center;
  color: $cor-quaternaria;
  background-color: $cor-primaria;
  border-top: 5px solid $cor-terciaria;
}
</style>
