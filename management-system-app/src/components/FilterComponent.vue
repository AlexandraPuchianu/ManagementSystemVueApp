<template>
  <div class="operations">
    <div class="sortEmployeesButtons">
      <button id="sortButton" sort="up" onClick="sortEmployeesByDate()">
        Sort employees by birthdate
      </button>
    </div>
    <div class="filterByGender">
      <label>Filter By Gender: </label>
      <select id="filterGender" required @change="filterEmployees()">
        <option value="" selected="selected">None</option>
        <option value="Male">Male</option>
        <option value="Female">Female</option>
        <option value="Other">Other</option>
      </select>
    </div>
    <div class="searchBar">
      <input
        type="text"
        id="inputSearchEmployees"
        @keyup="filterEmployees()"
        placeholder="Search for employees..."
      />
      <span class="searchIcon"><magnify-icon /></span>
    </div>
  </div>
</template>

<script>
import MagnifyIcon from "vue-material-design-icons/Magnify.vue";
import $ from "jquery";

export default {
  name: "FilterComponent",
  components: {
    MagnifyIcon,
  },
  props: {
    employeesTable: HTMLTableElement,
  },
  methods: {
    filterEmployees() {
      var genderFilter = $("#filterGender").val();
      var table = this.employeesTable;
      var tr = table.getElementsByTagName("tr");
      
      var input = document.getElementById("inputSearchEmployees");
      var searchInput = input.value.toUpperCase();
      
      for (var i = 0; i < tr.length; i++) {
        var nameCell = tr[i].getElementsByTagName("td")[0];
        var genderCell = tr[i].getElementsByTagName("td")[3];
        
        if (nameCell && genderCell) {
          var nameValue = nameCell.textContent || nameCell.innerText;
          var genderValue = genderCell.textContent || genderCell.innerText;
          if (
            genderValue.indexOf(genderFilter) > -1 &&
            nameValue.toUpperCase().indexOf(searchInput) > -1
          ) {
            tr[i].style.display = "";
          } else {
            tr[i].style.display = "none";
          }
        }
      }
    },
  },
};
</script>

<style scoped>
.operations {
  display: inline-flex;
}

.filterByGender {
  margin-left: 6rem;
  margin-top: 1rem;
}
.searchBar {
  display: inline-flex;
  margin-bottom: 0.5rem;
}

#inputSearchEmployees {
  width: 32%;
  font-size: 16px;
  padding: 0.7rem 0.5rem 0.2rem 1rem;
  border: 1px solid #ddd;
  margin-bottom: 1rem;
  margin-left: 21rem;
  border-right: none;
  border-radius: 0.5rem 0 0 0.5rem;
  margin-top: 0.5rem;
}

.searchIcon {
  padding: 8px 12px;
  font-size: 14px;
  color: #555;
  border: 1px solid #ccc;
  margin-bottom: 1rem;
  border-left: none;
  border-radius: 0 0.5rem 0.5rem 0;
  margin-top: 0.5rem;
}

button {
  background-color: #1a73e8;
  border: none;
  color: white;
  cursor: pointer;
  font-size: 1rem;
  margin-top: 0.5rem;
  height: 2rem;
  margin-left: 2rem;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
  border-radius: 4px;
}

.sortEmployeesButtons {
  margin-left: 1rem;
  margin-top: 0.5rem;
}
</style>
