<template>
  <div class="employeesList">
    <table id="employeesTable">
      <thead>
        <tr>
          <th>Profil Picture</th>
          <th>First name</th>
          <th>Last name</th>
          <th>Email</th>
          <th>Gender</th>
          <th>Birthdate</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody></tbody>
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
      this.$emit("tableOfEmployees", document.getElementById("employeesTable"));
    },
    appendRow(employee) {
      const row = document.createElement("tr");
      let tableNode = document.getElementById("employeesTable");
      row.style.cssText = "text-align:center";
      console.log(employee)
      for (const key in employee) {
        const cell = document.createElement("td");
        if (key === "id") {
          continue;
        }
        if (key === "birthdate") {
          cell.innerText = employee[key].split("T")[0];
        } else {
          cell.innerText = employee[key];
        }
        row.appendChild(cell);
      }
      if (tableNode.children.length < 2) {
        console.log("Table doesent contain body");
        return;
      }
      let button = document.createElement("button");
      button.innerHTML = "X";
      row.appendChild(button);
      button.onclick = function() {
        row.remove();
        $.ajax({
          method: "DELETE",
          url: `https://localhost:5001/employee/Employee/${employee.id}`,
          error: function() {
            alert(`Failed to remove employee from list`);
          },
        });
      };
      tableNode.children[1].appendChild(row);
      this.employeesList.push(employee);
    },
  },
};
</script>

<style scoped>
#employeesList {
  margin-top: 3rem;
  margin-left: 3rem;
}
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 80%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

#deleteBtn {
  background-color: #1a73e8;
  border: none;
  color: white;
  cursor: pointer;
  font-size: 1rem;
}
</style>
