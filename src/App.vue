<template>
  <ul>
    <li v-for="person in persons" :key="person.id">
      <img :src="require(`./assets/${person.id}.jpg`)">
    </li>
  </ul>
</template>

<script>
import persons from './assets/persons.json';

export default {
  name: 'App',
  data() {
    return {
      persons: persons
    }
  },
  components: {
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
