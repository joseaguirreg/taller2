<template>
    
  <v-card flat class="px-6">
    <v-card-text>
        <h1>LISTA DE TAREAS DE TODOS LOS USUARIOS</h1>


      <v-data-table
        :headers="headers"
        :items="tareas"
        
        :page.sync="page"
        :items-per-page="itemsPerPage"
        hide-default-footer
        class="elevation-1"
        @page-count="pageCount = $event"
      ></v-data-table>
      <div class="text-center pt-2">
        <v-pagination v-model="page" :length="pageCount"></v-pagination>
      </div>
      
    </v-card-text>
    
  </v-card>
  
</template>

<script>
import { mapState } from 'vuex'
import tareaService from "@/services/tarea.service";
export default {
  data() {
    return {
      page: 1,
      pageCount: 0,
      itemsPerPage: 10,
      headers: [
        { text: "ID", value: "id_usuario" },
        { text: "Título Tarea", value: "titulo" },
        { text: "Descripción tarea", value: "descripcion" },
      ],
      tareas: [],
    };
  },
  mounted() {
     this.getTareas();
  },
  methods: {
    getTareas() {
      tareaService
        .all()
        .then((response) => {
          this.tareas = response.data;
        })
        .catch((error) => {
          console.log(error.response.data.error);
        });
    },
  },
  computed: {
    ...mapState(["token","user"]),
   
    
   },
};
</script>