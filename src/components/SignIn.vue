<template>
  <modal
    title="Welcome Back"
    @close="closeModalValidate"
  >
    <!-- body -->
    <div slot="body">
      <form @submit.prevent="onSubmit">
        <!-- name -->
        <div class="form-item" :class="{ errorInput: $v.name.$error }">
          <label>Name:</label>
          <p class="errorText" v-if="!$v.name.required">Field is required</p>
          <input
            :class="{ error: $v.name.$error }"
            @change="$v.name.$touch()"
            v-model="name"
          />
        </div>
        
        <!-- password -->
        <div class="form-item" :class="{ errorInput: $v.password.$error }">
          <label>Password:</label>
          <p class="errorText" v-if="!$v.password.required">Field is required</p>
          <input
            :class="{ error: $v.password.$error }"
            @change="$v.password.$touch()"
            v-model="password"
          />
        </div>
        
        <!--button -->
        <div style="display: flex; justify-content: space-around; align-items: center;">
          <button class="btn btnPrimary">Sing In</button>
          <p class="navbar-link" @click="switchSingUp">Sign Up</p>
        </div>
      </form>
    </div>
  </modal>
</template>

<script>
  import {email, minLength, required, sameAs} from 'vuelidate/lib/validators'
  
  import modal from '../components/UI/Modal.vue'
  
  export default {
    name: "signIn",
    components: {
      modal
    },
    data() {
      return {
        name: '',
        password: '',
      }
    },
    validations: {
      name: {
        required
      },
      password: {
        required
      },
    },
    methods: {
      onSubmit () {
        this.$v.$touch()

        if (!this.$v.$invalid) {
          const user = {
            name: this.name,
            password: this.password
          }

          console.log(user)

          // Done!
          this.name = ''
          this.password = ''
          this.$v.$reset()
          this.$emit('close')
        }
      },
      closeModalValidate() {
        this.name = ''
        this.password = ''
        this.$v.$reset()
        this.$emit('close')
      },
      switchSingUp() {
        this.name = ''
        this.password = ''
        this.$v.$reset()
        this.$emit('switchSign', 'signUp')
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