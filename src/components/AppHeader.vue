<script>
export default {
  name: 'AppHeader'
}
</script>
<template>
  <header class="shadow">

    <nav class="nav justify-content-center">
      <router-link class="nav-link" :to="{ 'name': 'home' }" aria-current="page">Home</router-link>
      <router-link class="nav-link" :to="{ 'name': 'about' }">About</router-link>
      <router-link class="nav-link" :to="{ 'name': 'contacts' }">Contacts</router-link>
    </nav>
  </header>


</template>

<style lang="sass" scoped>

</style>


