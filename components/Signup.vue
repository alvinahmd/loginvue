<template>
   <v-app id="inspire">
      <v-main>
         <v-container fluid fill-height>
            <v-layout align-center justify-center>
               <v-flex xs12 sm8 md4>
                  <v-card class="elevation-12">
                     <v-card-text>
                        <v-form @signup.prevent="signup" ref="form">
                            <v-text-field
                              :rules="namadepanRules"
                              name="Masukan Nama Depan"
                              label="Masukan Nama Depan"
                              prepend-inner-icon="mdi-account"
                              type="text"
                              v-model="firstName"
                           ></v-text-field>
                           <v-text-field
                           :rules="namabelakangRules"
                              name="Masukan Nama Belakang"
                              label="Masukan Nama Belakang"
                              prepend-inner-icon="mdi-account"
                              type="text"
                              v-model="lastName"
                           ></v-text-field>
                           <v-text-field
                              :rules="emailRules"
                              name="email"
                              label="Masukan Email"
                              prepend-inner-icon="mdi-email"
                              type="text"
                              v-model="email"
                           ></v-text-field>
                           <v-text-field
                              :rules="passwordrules"
                              id="password"
                              name="password"
                              label="Masukan Password"
                              prepend-inner-icon="mdi-key"
                              :append-icon="passwordshow ? 'mdi-eye':'mdi-eye-off'"
                              @click:append="passwordshow = !passwordshow"
                              :type="passwordshow?'text':'password'"
                              v-model="password"
                           ></v-text-field>
                        </v-form>
                     </v-card-text>
                     <v-card-actions>
                        <v-spacer>
                        <v-btn block color="primary" @click="signupHandler">Daftar</v-btn>
                     </v-spacer>
                     </v-card-actions>
                     <v-col md=12>
                        <center>
                        <p>Sudah Punya Akun ? <router-link to="/login"> Klik Disini </router-link></p>
                        </center>
                  </v-col>
                  </v-card>
               </v-flex>
            </v-layout>
         </v-container>
      </v-main>
      <v-snackbar top color="green" v-model="snackbar">
			<center>Daftar Berhasil</center>
		</v-snackbar>
   </v-app>
</template>
<script>
 export default {
   name: 'signup',
    data: () => ({
      snackbar:false,
      valid: true,
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
     firstName: '',
     namadepanRules: [
        v => !!v || 'Nama Depan is required',
      ],
      lastName: '',
      namabelakangRules: [
        v => !!v || 'Nama Belakang is required',
      ],
      password: '',
      passwordrules: [
        v => !!v || 'Password is required',
      ],
      passwordshow:false 
    }),
   methods: {
      async signupHandler() {
         if(this.$refs.form.validate()){
            setTimeout( ()=> {
			this.snackbar = true
		})	
         }
         const data = {
            'first_name': this.firstName,
            'last_name': this.lastName,
            'email': this.email,
            'password': this.password
         }
         console.log(data);
         try {
             const res = await this.$axios.post('/register', data)
             console.log(res)
         }
         catch(e) {
             console.log(e.message)
         }
      }
   }
};
</script>
<style>
</style>
