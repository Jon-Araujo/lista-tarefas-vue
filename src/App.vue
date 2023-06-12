<template>
  <aside>
    <BarraLateral />
  </aside>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral
  }
});
</script>

<style lang="scss">
</style>
