<template>
  <v-container class="fill-height" fluid>
    <v-row class="flex-column" align="center" justify="center">
      <h1>Perfil</h1>
      <h2>Nombre: {{ user.firstName }}</h2>
      <h2>Apellido: {{ user.lastName }}</h2>
      <h2>Correo: {{ user.email }}</h2>
      <h2>Rol: {{ user.role }}</h2>
      <h2>ID: {{user._id}}</h2>
    </v-row>

    
  </v-container>
</template>

<script>
import Api from "@/services/api.service";
import { mapState } from 'vuex'
export default {
  data() {
    return {
      loginService: new Api("auth/login"),
      aux: {
        token: localStorage.getItem('token')
      }
    }
  },
  methods:{
    getId() {
     this.loginService((response)=>{
       const {user,token} = response.data;
       localStorage.getItem("user", JSON.stringify(user));
          localStorage.getItem("token", token);
         
        });
    }
  },
  computed: {
    ...mapState(["user"]),
  },
 
};
</script>
