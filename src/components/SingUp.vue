<template>
  <modal
    title="Sign Up Today"
    @close="closeModalValidate"
  >
    <!-- body -->
    <div slot="body">
      <form @submit.prevent="onSubmit">
        <!-- name -->
        <div class="form-item" :class="{ errorInput: $v.name.$error }">
          <label>Name:</label>
          <p class="errorText" v-if="!$v.name.required">Field is required</p>
          <p class="errorText" v-if="!$v.name.minLength">Name must have at least {{ $v.name.$params.minLength.min }} !</p>
          <input
            :class="{ error: $v.name.$error }"
            @change="$v.name.$touch()"
            v-model="name"
          />
        </div>
        
        <!-- email -->
        <div class="form-item" :class="{ errorInput: $v.email.$error }">
          <label>Email:</label>
          <p class="errorText" v-if="!$v.email.required">Field is required</p>
          <p class="errorText" v-if="!$v.email.email">Email is not correct!</p>
          <input
            :class="{ error: $v.email.$error }"
            @change="$v.email.$touch()"
            v-model="email"
          />
        </div>
        
        <!-- password -->
        <div class="form-item" :class="{ errorInput: $v.password.$error }">
          <label>Password:</label>
          <p class="errorText" v-if="!$v.password.required">Field is required</p>
          <p class="errorText" v-if="!$v.password.minLength">Password must have at least {{ $v.password.$params.minLength.min }} letters.</p>
          <input
            :class="{ error: $v.password.$error }"
            @change="$v.password.$touch()"
            v-model="password"
          />
        </div>
        
        <!-- repeatPassword -->
        <div class="form-item" :class="{ errorInput: $v.repeatPassword.$error }">
          <label>Repeat password:</label>
          <p class="errorText" v-if="!$v.repeatPassword.sameAsPassword">Passwords must be identical.</p>
          <input
            :class="{ error: $v.repeatPassword.$error }"
            @change="$v.repeatPassword.$touch()"
            v-model="repeatPassword"
          />
        </div>
        
        <!--button -->
        <div style="display: flex; justify-content: space-around; align-items: center;">
          <button class="btn btnPrimary">Sing Up</button>
          <p class="navbar-link" @click="switchSignIn">Sign In</p>
        </div>
        
      </form>
    </div>
  </modal>
</template>

<script>
  import { required, minLength, sameAs, email } from 'vuelidate/lib/validators'
  
  import modal from '../components/UI/Modal.vue'
  
  export default {
    name: "singUp",
    components: {
      modal
    },
    data() {
      return {
        name: '',
        email: '',
        password: '',
        repeatPassword: ''
      }
    },
    validations: {
      name: {
        required,
        minLength: minLength(4)
      },
      email: {
        required,
        email
      },
      password: {
        required,
        minLength: minLength(6)
      },
      repeatPassword: {
        sameAsPassword: sameAs('password')
      }
    },
    methods: {
      onSubmit () {
        this.$v.$touch()

        if (!this.$v.$invalid) {
          const user = {
            name: this.name,
            email: this.email,
            password: this.password
          }

          console.log(user)

          // Done!
          this.name = ''
          this.email = ''
          this.password = ''
          this.repeatPassword = ''
          this.$v.$reset()
          this.$emit('close')
        }
      },
      closeModalValidate() {
        this.name = ''
        this.email = ''
        this.password = ''
        this.repeatPassword = ''
        this.$v.$reset()
        this.$emit('close')
      },
      switchSignIn() {
        this.name = ''
        this.email = ''
        this.password = ''
        this.repeatPassword = ''
        this.$v.$reset()
        this.$emit('switchSign', 'signIn')
      }
    }
  }
</script>

<style lang="scss" scoped>
  .form-item .errorText {
    display: none;
    margin-bottom: 8px;
    font-size: 13.4px;
    color: red;
  }
  
  .form-item {
  &.errorInput .errorText {
     display: block;
   }
  }
  
  input.error {
    border-color: red;
  }
</style>