<template>
  <b-container>
    <b-row>
        <b-col offset-md="3" md="6">
          <b-card>
            <h6 slot="header" class="mb-0">Tropo Login</h6>
            
            <b-form method="post" @submit.prevent="login">

              <b-form-group horizontal label="Email">
                <b-form-input v-model="email" type="email" required></b-form-input>
              </b-form-group>

              <b-form-group horizontal label="Password">
                <b-form-input v-model="password" type="password" required></b-form-input>
              </b-form-group>

              <b-form-group horizontal>
                <b-button variant="primary" @click.prevent="login">Login</b-button>
                <span class="ml-3">
                  Don't have an account?
                  <nuxt-link to="/register">Register</nuxt-link>
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
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async login() {
      try {

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