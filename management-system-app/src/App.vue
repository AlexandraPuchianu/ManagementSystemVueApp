<template>
  <div id="app">
    <FormComponent @addEmployee = "addNewEmployee"/>
    <FilterComponent :employeesTable="employeesTable"/>
    <EmployeesListComponent @tableOfEmployees="onTableOfEmployeesClick" ref = "employees"/>
  </div>
</template>

<script>
import FormComponent from './components/FormComponent.vue'
import FilterComponent from './components/FilterComponent.vue'
import EmployeesListComponent from './components/EmployeesListComponent.vue'


export default {
  name: 'App',
  components: {
    FormComponent,
    FilterComponent,
    EmployeesListComponent
  },
  data() {
    return {
      employeesTable: HTMLTableElement
    }
  },
  methods: {
    addNewEmployee: function(data){
      this.$refs.employees.appendRow(data);
    },
    onTableOfEmployeesClick: function(value){
      this.employeesTable = value;
    }
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
