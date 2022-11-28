<template>
  <div id="app">
    <!-- <UserFormPage/> -->
  <!-- <NewUserForm/> -->
  <FormValidation/>
  </div>
</template>

<script>
//import NewUserForm from './components/NewUserForm.vue'
//import UserFormPage from './components/UserFormPage.vue'
import FormValidation from './components/FormValidation.vue'
export default {
  name: 'App',
  components: {
  // UserFormPage
   // NewUserForm
  FormValidation
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
