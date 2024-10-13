<template>
  <div class="row mt-5">
    <div class="col-md-6 offset-md-3">
      <div class="card">
        <div class="card-header bg-dark text-white text-center">
          Registrar Post
        </div>
        <div class="card-body">
          <form v-on:submit="guardar">
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
              <button class="btn btn-success"><i class="fa-solid fa-floppy-disk"></i> Registrar</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mostrarAlerta, enviarSolicitud } from '../funciones';

export default {
  data() {
    return {
      titulo: '',
      contenido: '',
      autor: '',
      url: 'http://127.0.0.1:8000/api/v1/posts',  
      cargando: false
    };
  },
  methods: {
    guardar(event) {
      event.preventDefault();
      
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
          autor: this.autor.trim(),
        };

        enviarSolicitud('POST', parametros, this.url, 'Post registrado con éxito!!!');
      }
    }
  }
};
</script>
