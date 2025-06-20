<!-- This page App.vue is similar to base.html in Django -->
<template>
  <div>
    <Navbar />
    <section class="section">
      <router-view /> <!-- Router view is similar to the block tag in Jinja 2-->
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import Navbar from './components/layout/Navbar.vue';
export default {
  name: 'App',
  components: {
    Navbar
  },
  beforeCreate() {
    this.$store.commit('initializeStore')
    if (this.$store.state.token) {
      axios.defaults.headers.common['Authorization'] = "Token " + this.$store.state.token
    } else {
      axios.defaults.headers.common['Authorization'] = ""
    }
  }
}
</script>

<style lang="scss">
@import '../node_modules//bulma';
</style>
