<template>
  <div id='employee-form'>
    <form @submit.prevent='handleSubmit'>
      <label>Employee name</label>
      <input v-model='employee.name' type="text">
      <label>Employee email</label>
      <input v-model='employee.email' type="text">
      <button>Add Employee</button>
    </form>

  </div>
</template>

<script>
export default {
  name: 'employee-form',

  data(){
    return{
      employee: {
      name: '',
      email: ''
    }
    }
  },

  methods: {
    handleSubmit(){
      this.$emit('add:employee', this.employee)
      this.employee= {name: '', email: ''}
    }
  }

}
</script>

<style>

</style>