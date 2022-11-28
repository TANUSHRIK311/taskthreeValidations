<template>
  <div>
<!-------------------------------NAV-BAR-SECTION-------------------------------------->

      <b-navbar toggleable type="dark" variant="dark">
  <b-navbar-brand href="#">User Data Form</b-navbar-brand>
      </b-navbar>
      <br/><br/>

<!---------------------------------FORM-SECTION---------------------------------->
<!------------------------------FIRST-NAME-SECTION-------------------------------->       
<b-form-row  @submit="login" @reset="onReset" class="border p-3">


  <b-col cols="6">
    <b-form-group
    id="first"
    label="First Name"
    label-for="firstName">
      
      <b-form-input id="firstName" type="text" placeholder="Enter your first name" v-model="firstname"></b-form-input>
      <p v-if="error1.length">
          <ul>
              <p v-for="e in error1" v-bind:key="e.id"  style="color:red;font-size:12px;text-align:center;" >
              {{e}}
              </p>
          </ul>
      </p><br/><br/> </b-form-group>
</b-col>
 

<!----------------------------------LAST-NAME-SECTION------------------------------>
  <b-col cols="6">
    <b-form-group
    id="second"
    label="Last Name"
    label-for="lastName">
  
      <b-form-input id="lastName" type="text" placeholder="Enter your last name" v-model="lastname">
      </b-form-input>
      <p v-if="error2.length">
          <ul>
              <p v-for="e in error2" v-bind:key="e.id" style="color:red;font-size:12px;text-align:center;" >
              {{e}}
              </p>
          </ul>
      </p><br/><br/>
    </b-form-group>
  </b-col>
<!-----------------------------------EMAIL-SECTION--------------------------------->
   <b-col cols="6">
    <b-form-group
    id="third"
    label="Email"
    label-for="EmailEmail">
    
  <b-form-input type="email" id="EmailEmail" placeholder="Enter your Email" v-model="$v.email.$model"  required></b-form-input>
  <div class="error" v-if="!$v.email.email" style="color:red;text-align:center;">* This must be an email</div>
  </b-form-group>
</b-col>

<!---------------------------------PHONE-NUMBER-SECTION------------------------------>
<b-col cols="6">
  <b-form-group id="fourth" label="Phone" label-for="PhonePhone">
   
   <b-form-input  placeholder="Enter Phone Number" type="number"
          id="PhonePhone"
          phone="fourth"
          v-model="$v.phone.$model"
          :state="validateState('phone')"
          aria-describedby="input-1-live-feedback">
        </b-form-input>
        <b-form-invalid-feedback
          id="input-1-live-feedback"
        >The Phone number must be equal to 10 Digits
      </b-form-invalid-feedback>
   </b-form-group>
  </b-col>


<!--------------------------------------BUTTONS------------------------------------------------------------------->

 <b-col cols="1"><b-button type="submit" variant="primary" @click="login">SUBMIT</b-button></b-col>
  <b-col cols="1"><b-button type="reset" variant="danger" @click="onReset">CLEAR</b-button></b-col>

</b-form-row>
  </div>
</template>

<!-------------------------------------SCRIPT-PART------------------------------------->
<!-------------------------------------SCRIPT-PART------------------------------------->
<!-------------------------------------SCRIPT-PART------------------------------------->
<script>
import { validationMixin } from "vuelidate";
import { required, minLength ,maxLength } from "vuelidate/lib/validators";
import email from 'vuelidate/lib/validators/email'
export default{
mixins: [validationMixin],
name:'UserDataForm',

data(){
return {
  error1:[],
  error2:[],
  firstname:null,
  lastname:null,
  phone:null,
  errorMessage:null,
   email: ""
  }
},
validations: {
     email: {
        email
      },
      phone: {
        required,
        minLength: minLength(10),
        maxLength: maxLength(10)
      }
  
},

methods:{
  validateState() {
      const { $dirty, $error } = this.$v.phone;
      console.log(this.$v.phone.$model)
      return $dirty ? !$error : null;
    },

status(validation) {
      return {
      error: validation.$error,
      dirty: validation.$dirty
    }
  },


  login(e)
  {
      if(this.firstname && this.lastname)
      {
      console.log("login function called");
      }
      this.error1=[];
      if(!this.firstname)
      {
      this.error1.push("* The First name is Required")
      }
      this.error2=[];
      if(!this.lastname)
      {
          this.error2.push("* The Last name is Required")
      }
      console.warn("errors",this.error)
     e.preventDefault()
  },

onReset(event) {
   event.preventDefault()
      // Clear The Form values
      this.firstname = ''
      this.lastname = ''
      this.phone = ''
      this.email = ''
      // Trick to reset/clear native browser form validation state
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    } 
}
}
</script>

<style>
body {
  padding: 1rem;
}
</style>