<template>
  <div>
    <h1 class="title position-title">{{ title }}</h1>
    
    <div class="authorization-content-wrp">
      
      <ul class="navbar-list">
        <li class="navbar-link" @click="signIn = !signIn">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-1"><path d="M15 3h4a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2h-4"></path><polyline points="10 17 15 12 10 7"></polyline><line x1="15" y1="12" x2="3" y2="12"></line></svg>
          Sing In
        </li>
        <li class="navbar-link" @click="signUp = !signUp">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-1"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path><circle cx="12" cy="7" r="4"></circle></svg>
          Sing Up
        </li>
      </ul>
      
      <signIn v-show="signIn" @switchSign="switchSign" @close="signIn = false"/>
      <singUp v-show="signUp" @switchSign="switchSign" @close="signUp = false"/>
  
      <img src="../assets/img/authorization.png" alt="authorization" width="914" height="403">
    </div>
    
  </div>
</template>

<script>
  import modalValidate from '../components/ModalValidate.vue'
  import signIn from '../components/SignIn.vue'
  import singUp from '../components/SingUp.vue'
  
  export default {
    name: "authorization",
    components: {
      modalValidate,
      signIn,
      singUp
    },
    data() {
      return {
        title: 'Authorization page',
        modalValidate: false,
        signIn: false,
        signUp: false
      }
    },
    methods: {
      switchSign(value) {

        switch (value) {
          case 'signIn':
            this.signIn = true
            this.signUp = false
            break
          case 'signUp':
            this.signUp = true
            this.signIn = false
            break
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  .authorization-content-wrp {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 50px;
    & ul {
      display: flex;
      justify-content: flex-end;
      width: 100%;
      margin-bottom: 20px;
    }
    & ul li {
      color: #5d5f61;
    }
  }
</style>