<template>
  <div id="employee-table">
    <table>
      <thead>
        <tr>
          <td>Employee Name</td>
          <td>Employee Email</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <td>{{ employee.name }}</td>
          <td>{{ employee.email }}</td>
          <td>
            <button @click="$emit('delete:employee', employee.id)">
              Delete
            </button>
            <button>Edit</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "employee-table",
  props: {
    employees: Array
  },

  methods: {}
};
</script>

<style lang="css" scoped></style>
