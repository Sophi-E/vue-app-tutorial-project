<template>
  <div id='employee-table'>
    <table>
      <thead>
        <tr>
          <td>Employee Name</td>
          <td>Employee Email</td>
          <td>Actions</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for ='employee in employees' :key='employee.id'>
          <td v-if ='editing === employee.id'>
          <input v-model='employee.name' type="text">
        </td>
          <td v-else>{{employee.name}}</td>
          <td v-if ='editing === employee.id'>
          <input v-model='employee.email' type="text">
        </td>
          <td v-else>{{employee.email}}</td>
          <td v-if ='editing === employee.id'>
          <button class='editing' @click='editEmployee(employee)'>Save</button>
          <button class='muted' @click='cancelEdit'>Cancel</button>
        </td>
          <td v-else><button @click='editMode(employee)'>Edit</button>
              <button @click='$emit("delete:employee", employee.id)'>Delete</button>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
export default {
name: 'employee-form',
props: {
  employees: Array
},

data(){
  return{
    editing: null,
  }
},

methods:{
  editMode(employee){
    const cachedEmployee = Object.assign({}, employee)
    this.editing = employee.id
  },
  editEmployee(employee){
    if(employee.name == '' || employee.email == '') return
    this.$emit('edit:employee', employee.id, employee)
    this.editing = null
  },
  cancelEdit(employee){
    Object.assign(employee, this.cachedEmployee)
    this.editing = null
  }
}
}
</script>

<style scoped>
.muted{
  background: #ccc;
  color: #333;
  outline: none;
  border: none;
}
.editing{
  background: #333;
  color: #ccc
}

</style>