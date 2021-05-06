<template>
  <div id="app">
    <FormComponent/>
    <FilterComponent/>
  </div>
</template>

<script>
import FormComponent from './components/FormComponent.vue'
import FilterComponent from './components/FilterComponent.vue'

export default {
  name: 'App',
  components: {
    FormComponent,
    FilterComponent
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: black;
}
</style>
