<template>
  <div class="modals-wrp">
    <h1 class="title position-title">{{ title }}</h1>
    
    <!-- first modal -->
    <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
    <modal
      title="First modal"
      v-show="modalFirst"
      @close="modalFirst = false"
    >
      <!-- body -->
      <div slot="body">
        <p style="margin-bottom: 20px;">Text first modal</p>
        <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Well Done!</button>
      </div>
    </modal>
    
    <!-- second modal -->
    <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show modal with form</button>
    <modal
      title="Modal with form"
      v-show="modalSecond.show"
      @close="modalSecond.show = false"
    >
      <!-- body -->
      <div slot="body">
        <form @submit.prevent="submitSecondForm">
          <label>Name:</label>
          <input type="text" v-model="modalSecond.name" required>
          <label>Email:</label>
          <input type="email" v-model="modalSecond.email" required>
          <button class="btn btnPrimary">Submit!</button>
        </form>
      </div>
    </modal>
    
    <!--  modal with validate  -->
    <button class="btn btnPrimary" @click="modalValidate = !modalValidate">Show modal with form + validate</button>
    <modalValidate v-show="modalValidate" @close="modalValidate = false" />
    
  </div>
</template>

<script>
  import modal from '../components/UI/Modal.vue'
  import modalValidate from '../components/ModalValidate.vue'
  
  export default {
    name: "modals",
    components: {
      modal,
      modalValidate,
    },
    data() {
      return {
        title: 'Modals Page',
        modalFirst: false,
        modalSecond: {
          show: false,
          name: '',
          email: ''
        },
        modalValidate: false,
      }
    },
    methods: {
      submitSecondForm() {
        console.log({
          name: this.modalSecond.name,
          email: this.modalSecond.email
        })

        this.modalSecond.name = ''
        this.modalSecond.email = ''
        this.modalSecond.show = false
      }
    }
  }
</script>

<style lang="scss" scoped>
  .modals-wrp {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
    height: 250px;
  }
</style>