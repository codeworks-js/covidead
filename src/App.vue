<template>
  <div class="covidead">
    <h1>Covidead</h1>
    <p>Data fetched from <a href="https://covid19api.com/" target="_blank">covid19api</a>.</p>
    <CovidStats />
  </div>
</template>

<script>
import CovidStats from './components/CovidStats.vue'

export default {
  name: 'App',
  components: {
    CovidStats
  }
}
</script>

<style scoped>
.covidead {
  display: flex;
  flex-flow: column;
  align-items: center;
  min-width: 100%;
}
</style>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}
</style>