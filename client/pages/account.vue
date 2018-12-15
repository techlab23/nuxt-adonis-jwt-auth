<template>
  <b-container>
    <b-row>
        <b-col offset-md="3" md="6">
          <b-card>
            <h6 slot="header" class="mb-0">Tropo Account</h6>

            <div class="card-text">
              <p>
                Username: {{ loggedInUser.username }}
              </p>  
              <p>
                Email: {{ loggedInUser.email }}
              </p>  
            </div>
            
          </b-card>
        </b-col>
      </b-row>
    </b-container>
</template>

<script>
/* eslint-disable */
import { mapGetters } from 'vuex'
export default {
  middleware: 'auth',
  data () {
    return {}
  },
  computed: {
    ...mapGetters(['loggedInUser'])
  }
}
</script>

<style scoped>

</style>