<template>
    <form id="form" onsubmit="return false">
        <label>First name: </label>
        <input type="text" id="fname" placeholder="First name"><br><br>
        <label>Last name: </label>
        <input type="text" id="lname" placeholder="Last Name"><br><br>
        <label>Email: </label>
        <input type="text" id="email" placeholder="Email"><br><br>
        <label>Gender:</label>
        <select id="gender">
            <option value="Male">Male</option>
            <option value="Female">Female</option>
            <option value="Other">Other</option>
        </select><br><br>
        <label>Birthdate: </label>
        <input type="date" id="birthdate" value="2003-01-01" min="1921-01-01" max="2021-04-23"><br><br>
        <label>Picture:</label>
        <input type="file" id="picture" onchange="upload(this)"><br><br>
        <button type="submit" class="submitButton" @click="addEmployee()">Submit</button>
    </form>
</template>

<script>
import $ from "jquery";

export default {
    name: 'FormComponent',
    methods: {
    validateInput(newEmployee) {
      if (
        !newEmployee.firstName ||
        !newEmployee.lastName ||
        !newEmployee.email ||
        !newEmployee.birthdate
      ) {
        return false;
      }
      return true;
    },
    addEmployee() {
      var self = this;
      
      var newEmployee = new Object();
      newEmployee.firstName = document.getElementById("fname").value;
      newEmployee.lastName = document.getElementById("lname").value;
      newEmployee.email = document.getElementById("email").value;
      newEmployee.gender = document.getElementById("gender").value;
      newEmployee.birthdate = document.getElementById("birthdate").value;
      
      if (!this.validateInput(newEmployee)) {
        alert("Fields are required.");
        return
      }

      $.ajax({
        method: "POST",
        contentType: "application/json",
        data: JSON.stringify(newEmployee),
        url: "https://localhost:5001/employee/Employee",
        success: function(data) {
            self.$emit('addEmployee', data);
        },
        error: function() {
          alert(`Failed to add employee.`);
        },
      });
    },
  },
}
</script>

<style scoped>
form{
    margin-top: 3rem;
    margin-left: 3rem;
}

.submitButton{
    background-color: #1a73e8;
    border: none;
    color: white;
    margin-left: 1.5rem;
    text-decoration: none;
    font-size: 14px;
    cursor: pointer;
    height: 2.3rem;
    padding-left: 1.5rem;
    padding-right: 1.5rem;
    border-radius: 4px;
}
</style>