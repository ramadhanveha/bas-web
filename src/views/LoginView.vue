<script setup>
import {inject,reactive} from 'vue';
import router from "@/router/index"
import { useAuthStore } from '@/stores/auth';

const auth = useAuthStore()

const data = reactive({
    username: "",
    password:"",
    snackbar:false,
    pesanLogin: "",
})

const myAxios = inject('myAxios')



const login = () => {
    console.log("login clicked",data);
    myAxios.post("/transaction/transfer-bank",{
      username:data.username,
      password:data.password
    }).then((res) => {
      if(res.status==200){
        data.pesanLogin="Anda Berhasil Login"
        auth.authenticated()
        router.push('about')
      }
      data.snackbar= true
    }, (err) => {
      data.pesanLogin = "Username atau password salah"
      data.snackbar = true
    })
     
}
</script>
<template>
    <v-card class="pa-3">
    <div class="container">
        <div>
            <label>Username</label>
            <v-text-field type="text" v-model="data.username"/>
        </div>
        <div>
            <label>Password</label>
            <v-text-field type="password" v-model="data.password"/>
        </div>
        <v-btn @click="login">
  Button
</v-btn>
    </div>
</v-card>

<div class="text-center ma-2">
   
    <v-snackbar
      v-model="data.snackbar"
    >
      {{ data.pesanLogin }}

      <template v-slot:actions>
        <v-btn
          color="pink"
          variant="text"
          @click="data.snackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

