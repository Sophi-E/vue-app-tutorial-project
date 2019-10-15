<template>
  <div id='app'>
    <h1>Employees</h1>
    <employee-form @add:employee='addEmployee' />
    <employee-table 
     :employees='employees' 
     @delete:employee='deleteEmployee'
     @edit:employee='editEmployee' />

  </div>
</template>

<script>
import EmployeeTable from './components/EmployeeTable.vue'
import EmployeeForm from './components/EmployeeForm.vue'
import uuid from 'uuid'

export default {
  name: 'app',
  components:{
    EmployeeTable,
    EmployeeForm
  },

  data(){
    return{
      employees:[
        {
        id: uuid(),  
        name: 'Sophia Enax',
        email: 'enax@gmail.com'
        },
        {
        id: uuid(),  
        name: 'Goodness Amadi',
        email: 'amadig@gmail.com'
        },
        {
        id: uuid(),  
        name: 'Chioma Beke',
        email: 'chioma@gmail.com'
        }
      ]
    }
  },

  methods:{
    addEmployee(employee){
      const id = uuid()
      const newEmployee = {...employee, id}
      this.employees =[...this.employees, newEmployee]
    },

    deleteEmployee(id){
      this.employees = this.employees.filter(employee => employee.id !== id)
    },

    editEmployee(id, updatedEmployee){
      this.employees = this.employees.map(employee.id === id ? updatedEmployee : employee)
    }
  }

}
</script>

<style>
body{
  padding: 20px;
  width: 70%;
  margin: auto;
}

</style>