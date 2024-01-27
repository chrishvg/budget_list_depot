<template>
  <BudgetSummary />
</template>

<script>
import BudgetSummary from './components/BudgetSummary.vue'

export default {
  name: 'App',
  components: {
    BudgetSummary,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
