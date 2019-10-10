<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form @add:employee="addEmployee" />
    <employee-table :employees="employees" @delete:employee="deleteEmployee" />
  </div>
</template>

<script>
import uuid from 'uuid';
import EmployeeForm from "./components/EmployeeForm.vue";
import EmployeeTable from "./components/EmployeeTable.vue";

export default {
  name: "app",
  components: {
    EmployeeForm,
    EmployeeTable
  },

  data() {
    return {
      employees: [
        {
          id: uuid(),
          name: "Richard Hendricks",
          email: "richard@piedpiper.com"
        },
        {
          id: uuid(),
          name: "Bertram Gilfoyle",
          email: "gilfoyle@piedpiper.com"
        },
        {
          id: uuid(),
          name: "Dinesh Chugtai",
          email: "dinesh@piedpiper.com"
        }
      ]
    };
  },

  methods: {
    addEmployee(employee) {
      const id = uuid()
      const NewEmployee = { ...employee, id };
      this.employees = [...this.employees, NewEmployee]; 
    },
    deleteEmployee(id) {
      this.employees = this.employees.filter(employee => {
        employee.id !== id;
      });
    }
  }
};
</script>

<style></style>
