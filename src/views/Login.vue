<template>
  <v-layout class="background mt-5">
    <div style="margin: 130px auto">
      <v-card max-width="400" flat>
        <v-card-title class="justify-center">
          <h2>Login</h2>
        </v-card-title>
        <div class="mr-5 ml-5" />
        <v-card-text>
          <v-form ref="form" class="px-3">
            <v-text-field
              v-model="username"
              outlined
              label="username"
              :prepend-icon="mdiAccount"
              :rules="inputRules"
              autocomplete="current email"
              name="username"
              autocapitalize="none"
              @keyup.enter.native="login"
            />
            <v-text-field
              v-model="password"
              outlined
              type="password"
              label="password"
              :prepend-icon="mdiLock"
              :rules="inputRules"
              autocomplete="current password"
              name="password"
              autocapitalize="none"
              @keyup.enter.native="login"
            />
            <v-spacer />
            <v-card-actions class="justify-center">
              <v-btn
                text
                class="accent white--text mx-0 mt-3"
                @click="login"
              >
                Login
              </v-btn>
            </v-card-actions>
          </v-form>
        </v-card-text>
      </v-card>
    </div>
  </v-layout>
</template>

<script>
import { mdiLock, mdiAccount } from '@mdi/js'
import { isAuthenticated } from '@/services/auth.js'

export default {
  name: 'Login',
  data() {
    return {
      username: '',
      password: '',
      inputRules: [v => v.length >= 1 || 'At least 1 character'],
      mdiLock, mdiAccount
    }
  },
  mounted() {
    if (isAuthenticated()) {
      this.$router.push('/')
    }
  },
  methods: {
    async login() {
      const authenticated = await this.$store.dispatch('LOGIN', {
        username: this.username,
        password: this.password
      })

      if (authenticated) {
        this.$router.push('/')
      }
    }
  }
}
</script>
