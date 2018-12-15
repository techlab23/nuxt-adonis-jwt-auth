<template>
  <b-navbar toggleable="md" variant="faded" type="light">
    <b-navbar-brand href="/">TROPO</b-navbar-brand>
    <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

    <b-collapse is-nav id="nav_collapse">
      <b-navbar-nav class="ml-auto">
        <b-nav-item-dropdown right>
            <template slot="button-content" v-if="isAuthenticated">
              <em>{{ loggedInUser.username }}</em>
            </template>
            <template slot="button-content" v-else>
              <em>User</em>
            </template>
            <div v-if="isAuthenticated">
              <b-dropdown-item href="/account" >Account</b-dropdown-item>
              <b-dropdown-item @click="logout" >Logout</b-dropdown-item>
            </div>
            <div v-else>
              <b-dropdown-item href="/register" v-if="!isAuthenticated">Register</b-dropdown-item>  
              <b-dropdown-item href="/login" v-if="!isAuthenticated">Login</b-dropdown-item>  
            </div>
        </b-nav-item-dropdown>
      </b-navbar-nav>
  </b-collapse>
  </b-navbar>
</template>

<script>
/* eslint-disable */
import { mapGetters } from 'vuex'
export default {
  data () {
    return {}
  },
  computed: {
    ...mapGetters(['isAuthenticated', 'loggedInUser'])
  },
  methods: {
    async logout() {
      await this.$auth.logout()
      this.$router.push('/login')
    },
  }
}
</script>

<style scoped>

</style>