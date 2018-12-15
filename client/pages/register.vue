<template>
  <b-container>
    <b-row>
        <b-col offset-md="3" md="6">
          <b-card>
            <h6 slot="header" class="mb-0">Tropo Registration</h6>
            <b-form method="post" @submit.prevent="register">

              <b-form-group horizontal label="User name">
                <b-form-input v-model="username" type="text" required></b-form-input>
              </b-form-group>
              <b-form-group horizontal label="Email">
                <b-form-input v-model="email" type="email" required></b-form-input>
              </b-form-group>
              <b-form-group horizontal label="Password">
                <b-form-input v-model="password" type="password" required></b-form-input>
              </b-form-group>
              <b-form-group horizontal>
                <b-button variant="primary" @click.prevent="register">Register</b-button>
                <span class="ml-3">
                  Already got an account? 
                  <nuxt-link to="/login">Login</nuxt-link>
                </span>
              </b-form-group>
              <b-alert :show="error !== null" variant="danger">{{ error }}</b-alert>              
            </b-form>
          </b-card>
        </b-col>
    </b-row>
  </b-container>
</template>

<script>
/* eslint-disable */
export default {
  middleware: 'guest',
  data () {
    return {
      username: '',
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register() {
      try {
        await this.$axios.post('register', {
          username: this.username,
          email: this.email,
          password: this.password
        })

        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })
        this.$router.push('/')

      } catch (e) {
        this.error = e.response.data.message
      }

    }
  }
}
</script>

<style scoped>

</style>