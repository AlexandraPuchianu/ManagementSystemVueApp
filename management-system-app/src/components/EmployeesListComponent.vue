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

import $ from "jquery";
export default {   
    name: "EmployeesListComponent",   
    data() {     
        return {       
            employeesList: [],     
        };   
    },   
    async created() {     
        let self = this;     
        $.ajax({       
            method: "GET",       
            url: "https://localhost:5001/employee/Employee",       
            success: function(data) {         
                this.employeesList = data;         
                self.loadEmployees(this.employeesList);       
            },       
            error: function() {         
                alert(`Failed to get employees list.`);       
            },     
        });   
    },   
    methods: {     
        loadEmployees(employeesList) {       
            for (var index = 0; index < employeesList.length; index++) {         
                this.appendRow(employeesList[index]);       
            }     
        },     
        appendRow(employee) {       
            let employeesTable = document.querySelector("table");
            let newRow = ` <tr>
                            <td id="picture">pic
                            <td id="firstName">${employee.firstName}</td>
                            <td id="lastName">${employee.lastName}</td>
                            <td id="email">${employee.email}</td>
                            <td id="gender">${employee.gender}</td>
                            <td id="birthdate">${employee.birthdate}</td>
                            <td><button onclick="this.deleteUser($event.target, ${employee.id})" id="deleteBtn"><i class="fab fa-close"></i></i></button></td>
                        </tr>`;
                
        employeesTable.innerHTML += newRow;
        }, 
    }    
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