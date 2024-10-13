<template>
  <div class="row mt-3">
    <div class="col-md-6 offset-md-3">
      <div class="card">
        <div class="card-header bg-dark text-white text-center">
          Editar Post
        </div>
        <div class="card-body">
          <form v-on:submit.prevent="actualizar">
            <div class="input-group mb-3">
              <span class="input-group-text"><i class="fa-solid fa-heading"></i></span>
              <input type="text" v-model="titulo" id="titulo" placeholder="Ingrese el Título" maxlength="100" class="form-control">
            </div>
            <div class="input-group mb-3">
              <span class="input-group-text"><i class="fa-solid fa-align-left"></i></span>
              <textarea v-model="contenido" id="contenido" placeholder="Ingrese el Contenido" class="form-control" rows="5"></textarea>
            </div>
            <div class="input-group mb-3">
              <span class="input-group-text"><i class="fa-solid fa-user"></i></span>
              <input type="text" v-model="autor" id="autor" placeholder="Ingrese el Autor" maxlength="50" class="form-control">
            </div>
            <div class="d-grid col-6 mx-auto mb-3">
              <button class="btn btn-success"><i class="fa-solid fa-floppy-disk"></i> Actualizar</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mostrarAlerta, enviarSolicitud, confirmarActualizacion } from '../funciones';
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
      axios.get(this.url).then(res => {
        this.titulo = res.data.data.titulo;
        this.contenido = res.data.data.contenido;
        this.autor = res.data.data.autor;
      }).catch(error => {
        console.error("Error al obtener los posts:", error);
      });
    },
    actualizar() {
    // Previene el comportamiento por defecto del formulario
    event.preventDefault(); 

    // Validar campos antes de confirmar
    if (this.titulo.trim() === '') {
        mostrarAlerta('Ingrese un Título', 'warning', 'titulo');
    } else if (this.contenido.trim() === '') {
        mostrarAlerta('Ingrese el Contenido', 'warning', 'contenido');
    } else if (this.autor.trim() === '') {
        mostrarAlerta('Ingrese un Autor', 'warning', 'autor');
    } else {
        const parametros = {
            titulo: this.titulo.trim(),
            contenido: this.contenido.trim(),
            autor: this.autor.trim()
        };
        
        // Llama a confirmarActualizacion en lugar de enviarSolicitud
        confirmarActualizacion(this.url, this.id, 'Confirmar Actualización', '¿Está seguro que desea actualizar este post?', parametros, () => {
        this.getPosts(); // Recarga los datos después de actualizar
        console.log('Callback de confirmación ejecutado');
      });
    }
}

  }
};
</script>
