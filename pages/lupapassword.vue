<template>
    <v-container >
        <v-layout style="margin-top: 400;margin-left:400px;padding-top:150px;">
          <v-flex sm14 md7 offset-md5>
            <v-card class="elevation-12">
              <v-col>
                <v-row>
                    <v-text-field
                    :rules="emailRules"
                    name="email"
                    label="Masukan Email"
                    type="text"
                    v-model="email"
                 ></v-text-field>
                    <v-spacer>
                    <v-btn block color="primary" @click="KirimHandler">Kirim Email</v-btn>
                 </v-spacer>
                    <v-col md=12>
                        <center>
                        <p>Login kembali ? <router-link to="/login"> Klik Disini </router-link></p></center>
                    </v-col>
                </v-row>
              </v-col>
            </v-card>
          </v-flex>
        </v-layout>
    </v-container>
</template>
<script>
export default {
    data: () => ({
      valid: true,
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],}
    )
    }
</script>
