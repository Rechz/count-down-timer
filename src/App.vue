<template>
  <CountDown/>
</template>

<script>
import CountDown from './components/CountDown.vue';
export default {
  name: 'App',
  components: {
     CountDown
  }
}
</script>
<style>
body {
  background: radial-gradient(circle, #180639, #080015);
}
</style>
