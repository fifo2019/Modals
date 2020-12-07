<template>
  <div class="wrapper">
    <div class="wrapper-content">
  
      <navigation :navigation="navigation" @switch="navigationSwitch" />
      
      <section style="margin: 100px 0 0 0;">
        <div class="container">
          
          <div v-show="navigation.home" style="display: flex;">
            <h1 class="title position-title">{{ title }}</h1>
            <img src="./assets/img/home-img.jpg" alt="home page" width="614" height="357">
          </div>
          
          
          <modals v-show="navigation.modals" />
          
          <authorization v-show="navigation.authorization" />
          
          
        </div>
      </section>
      
      
      
    </div>
  </div>
</template>

<script>
import navigation from './components/Navigation.vue'
import authorization from './components/Authorization.vue'
import modals from './components/Modals.vue'

export default {
  name: 'App',
  components: {
    navigation,
    modals,
    authorization
  },
  data() {
    return {
      title: 'Home page',
      navigation: {
        home: true,
        modals: false,
        authorization: false,
      }
    }
  },
  methods: {
    navigationSwitch(value) {

      this.navigation.home = false
      this.navigation.modals = false
      this.navigation.authorization = false
      
      switch (value) {
        case 'home':
          this.navigation.home = true
          break
        case 'modals':
          this.navigation.modals = true
          break
        case 'authorization':
          this.navigation.authorization = true
          break
      }
    }
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
