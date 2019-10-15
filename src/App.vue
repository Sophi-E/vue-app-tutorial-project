<template>
  <div id='app'>
    <h1>Employees</h1>
    <employee-form @add:employee = 'addEmployee'/>
    <employee-table :employees ='employees'
    @delete:employee = 'deleteEmployee'
    @edit:employee = 'editEmployee'
    />
    
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
      employees:[]
    }
  },

  methods:{
    async addEmployee(employee){
      try{
        const response = await fetch('https://jsonplaceholder.typicode.com/users',{
        method: 'POST',
        body: JSON.stringify(employee),
        headers: {'Content-type': 'application/json; charset=UTF-8'}
        })
      
      const data = await response.json()
      this.employees = [...this.employees, data]
      }catch(error){
        console.log(error)
      }
    },

    async deleteEmployee(id){
      try{
        const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`,{
          method: 'DELETE',
        });
      this.employees = this.employees.filter(employee => employee.id !== id)
      }catch(error){
        console.log(error);
      }
    },

     async editEmployee(id, updatedEmployee){
       try{
         const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`,{
           method: 'PUT',
           body: JSON.stringify(updatedEmployee),
           headers: { 'Content-type': 'application/json; charset=UTF-8' },
         })
         const data = await response.json()
       this.employees = this.employees.map(employee => employee.id === id ? data : employee)
       }catch(error){
         console.log(error)
       }
     },

//     async editEmployee(id, updatedEmployee) {
//   try {
//     const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
//       method: 'PUT',
//       body: JSON.stringify(updatedEmployee),
//       headers: { 'Content-type': 'application/json; charset=UTF-8' },
//     })
//     const data = await response.json()
//     this.employees = this.employees.map(employee => (employee.id === id ? data : employee))
//   } catch (error) {
//     console.error(error)
//   }
// },
//get request
    async getEmployees(){
      try{
        const response = await fetch('https://jsonplaceholder.typicode.com/users')
        const data = await response.json()
        this.employees = data
      }catch(error){
        console.log(error)
      }
    }
  },

  mounted(){
    this.getEmployees()
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