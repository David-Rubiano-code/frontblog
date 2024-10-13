<template>
  <div style="margin-top: 80px;"> <!-- Ajusta el valor según sea necesario -->
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <div class="card">
          <div class="card-header bg-dark text-white text-center">
            Detalles del Post
          </div>
          <div class="card-body">
            
            <div class="input-group mb-3">
              <span class="input-group-text"><i class="fa-solid fa-heading"></i></span>
              <label v-text="titulo" class="form-control"></label>
            </div>
            <div class="input-group mb-3">
              <span class="input-group-text"><i class="fa-solid fa-align-left"></i></span>
              <textarea v-text="contenido" class="form-control" rows="5"></textarea>
            </div>
            <div class="input-group mb-3">
              <span class="input-group-text"><i class="fa-solid fa-user"></i></span>
              <label v-text="autor" class="form-control"></label>
            </div>
            <div class="d-grid col-6 -mx-auto mb-3">
              <router-link to="/viewP" class="btn  btn-warning btn-sm mx-1">
                <i class="fa-solid fa-arrow-left"></i> Regresar a la lista
              </router-link>
            </div> 
          </div>
        </div>
      </div>
    </div>
  </div>
</template>



<script>
import { useRoute } from 'vue-router';
import axios from 'axios';

export default {
  data() {
    return {
      id: 0,
      titulo: '',
      contenido: '',
      autor: '',
      url: 'http://127.0.0.1:8000/api/v1/posts',  
      cargando: false
    };
  },
  mounted() {
    const route = useRoute();
    this.id = route.params.id;
    this.url += '/' + this.id;
    this.getPosts();
  },
  methods: {
    getPosts() {
      this.cargando = true;  // Establecer el estado de carga
      axios.get(this.url)
        .then(res => {
          this.titulo = res.data.data.titulo;
          this.contenido = res.data.data.contenido;
          this.autor = res.data.data.autor;
        })
        .catch(error => {
          console.error("Error al obtener el post:", error);
        })
        .finally(() => {
          this.cargando = false;  // Resetear el estado de carga
        });
    },
  }
};
</script>
