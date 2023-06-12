<template>
  <div id="app">
    <BestTransport/>
    <DivDestinoPeso/>
  </div>
</template>

<script>
import BestTransport from './components/BestTransport.vue'
import DivDestinoPeso from './components/DivDestinoPeso.vue';

export default {
  name: 'App',
  components: {
    BestTransport,
    DivDestinoPeso,
}
}
</script>

<style>
</style>
