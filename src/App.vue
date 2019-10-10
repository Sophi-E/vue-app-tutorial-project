<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form @add:employee="addEmployee" />
    <employee-table :employees="employees" @delete:employee="deleteEmployee" />
  </div>
</template>

<script>
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
          id: 1,
          name: "Richard Hendricks",
          email: "richard@piedpiper.com"
        },
        {
          id: 2,
          name: "Bertram Gilfoyle",
          email: "gilfoyle@piedpiper.com"
        },
        {
          id: 3,
          name: "Dinesh Chugtai",
          email: "dinesh@piedpiper.com"
        }
      ]
    };
  },

  methods: {
    addEmployee(employee) {
      const LastId =
        this.employees.length > 0
          ? this.employees[this.employees.length - 1].id
          : 0;
      const Id = LastId + 1;
      const NewEmployee = { ...employee, Id };
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
