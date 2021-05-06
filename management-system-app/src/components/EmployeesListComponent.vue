<template>
    <div class="employeesList">
        <table id="employeesTable">
            <tr>
                <th>Profil Picture</th>
                <th>First name</th>
                <th>Last name</th>
                <th>Email</th>
                <th>Gender</th>
                <th>Birthdate</th>
                <th></th>
            </tr>
          </table>
    </div>
</template>

<script>
export default {
    name: 'EmployeesListComponent',
}
</script>

<style scoped>
#employeesList{
    margin-top: 3rem;
    margin-left: 3rem;
}
table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 80%;
  }
  
  td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }
  
  tr:nth-child(even) {
    background-color: #dddddd;
  }

  #deleteBtn{
    background-color: #1a73e8;
    border: none;
    color: white;
    cursor: pointer;
    font-size: 1rem;
  }
</style>