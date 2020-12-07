<template>
  <nav class="navbar">
    <ul class="navbar-list">
      <li
        class="navbar-link"
        :class="{ active: navigation.home }"
        @click="$emit('switch', 'home')"
      >
        Home
      </li>
      <li
        class="navbar-link"
        :class="{ active: navigation.modals }"
        @click="$emit('switch', 'modals')"
      >
        Modals
      </li>
      <li
        class="navbar-link"
        :class="{ active: navigation.authorization }"
        @click="$emit('switch', 'authorization')"
      >
        Authorization
      </li>
    </ul>

  </nav>
</template>

<script>
  export default {
    name: "navigation",
    props: {
      navigation: {
        type: Object,
        required: true,
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>