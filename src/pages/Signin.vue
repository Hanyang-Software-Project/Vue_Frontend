<template>
    <div id="signinForm" class="formContainer">
        <FormComponent
        title="Create account" submit-text="Sign in"
        :onSubmit="onSigninFormSubmit"
        >
            <LabelledInput input-type="text" label="Username" input-place-holder="myUsername" v-model="username" />
            <LabelledInput input-type="text" label="Email" input-place-holder="myaddress@mail.com" v-model="email"/>
            <LabelledInput input-type="password" label="Password" input-place-holder="**********" v-model="password"/>
            <LabelledInput input-type="text" label="Phone number" input-place-holder="0123456789" v-model="phone"/>
            <LabelledInput input-type="text" label="House name" input-place-holder="My Home" v-model="houseName"/>
            <LabelledInput input-type="text" label="House address" input-place-holder="221B Baker Street, London" v-model="address"/>
        </FormComponent>
        <div class="loginLink">
          <router-link :to="{name: 'loginPage'}">I already have an account</router-link>
        </div>
    </div>
</template>
<script>
import FormComponent from '@/components/FormComponent.vue';
import LabelledInput from '@/components/Inputs/LabelledInput.vue';

export default{
  components: {
    FormComponent, LabelledInput
  },
  data() {
    return {
      email: '',
      username: '',
      password: '',
      phone: '',
      houseName: '',
      address: ''
    }
  },
  methods: {
    onSigninFormSubmit(){
      const body = {
        email: this.email,
        username: this.username,
        password: this.password,
        phoneNumber: this.phone,
        house: {
          houseName: this.houseName,
          address: this.address
        }
      }

      fetch('http://localhost:8080/users/create-user', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(body)
      })
      .then(res => res.json())
      .then(jsonRes => {
        if(jsonRes.code == 201)
          this.$router.push({name: 'loginPage'})
        else
          console.log('error: ' + jsonRes)
      })
      .catch(_ => {
        console.log('Signin error')
      })
    }
  }
}
</script>
