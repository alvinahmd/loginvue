<!-- eslint-disable no-tabs -->
<template>
  <v-app>
    <div class="background" />
    <v-main>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-12">
              <div class="text-center pt-6">
                <v-avatar size="100" color="indigo lighten-4">
                  <v-icon size="55" color="indigo">
                    mdi-account
                  </v-icon>
                </v-avatar>
              </div>
              <v-card-text>
                <v-form ref="form" @login.prevent="loginHandler">
                  <v-text-field
                    v-model="email"
                    name="email"
                    :rules="emailRules"
                    label="Masukan E-mail"
                    prepend-inner-icon="mdi-email"
                    required
                  />
                  <v-text-field
                    id="password"
                    v-model="password"
                    :rules="passwordRules"
                    :type="passwordshow?'text':'password'"
                    placeholder="password"
                    label=" Masukan Password"
                    :append-icon="passwordshow ? 'mdi-eye':'mdi-eye-off'"
                    @click:append="passwordshow = !passwordshow"
                  />
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer />
                <v-btn block color="primary" @click="loginHandler">
                  Login
                </v-btn>
              </v-card-actions>
              <v-card-actions>
                <v-spacer />
                <v-btn block color="primary" @click="redirectSignup()">
                  Daftar
                </v-btn>
              </v-card-actions>
              <v-col md="12">
                <center>
                  <p>
                    Lupa Password ? <router-link to="./lupapassword">
                      Klik Disini
                    </router-link>
                  </p>
                </center>
              </v-col>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-main>
    <v-snackbar v-model="snackbar" top color="green">
      <center>Login Berhasil</center>
    </v-snackbar>
  </v-app>
</template>
<script>
// eslint-disable-next-line no-unused-vars
import Signup from './Signup.vue'

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Login',
  data: () => ({
    snackbar: false,
    valid: true,
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
    ],
    password: '',
    passwordRules: [
      v => !!v || 'password is required'
    ],
    passwordshow: false
  }),

  methods: {
    async loginHandler () {
      if (this.$refs.form.validate()) {
        setTimeout(() => {
          this.snackbar = true
        })
      }
      const data = { email: this.email, password: this.password }
      console.log(data)
      try {
        const response = await this.$auth.loginWith('local', { data })
        console.log(response)
        this.$auth.$storage.setUniversal('email', response.data.email)
        await this.$auth.setUserToken(response.data.access_token, response.data.refresh_token)
      } catch (e) {
        console.log(e.message)
      }
    },
    redirectSignup () {
      this.$router.push('/signup')
    }

  }
}

</script>
<style>
.background{
background-image: url(./assets/gambar.jpg) !important;
height: 300px;
width: 1400px;
display:block;
position:absolute;
top: 0%;
background-size:cover;
}
</style>
