<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-lg-8 offset-lg-2">
        <div class="table-responsive">
          <br />
          <table class="table table-bordered table-striped table-hover">
            <thead class="table-dark">
              <tr>
                <th>#</th>
                <th>ID</th>
                <th>TITULO</th>
                <th class="w-50">CONTENIDO</th>
                <th>AUTOR</th>
                <th>REGISTRO</th>
                <th>ACCIONES</th>
              </tr>
            </thead>
            <tbody class="table-group-divider" id="contenido">
              <tr v-if="cargando">
                <td colspan="7">
                  <h3 class="text-center">Cargando...</h3>
                </td>
              </tr>
              <tr v-else v-for="(pos, i) in posts" :key="pos.id">
                <td v-text="(i+1)"></td>
                <td v-text="pos.id"></td>
                <td v-text="pos.titulo"></td>
                <td class="text-truncate" style="max-width: 250px;" v-text="pos.contenido"></td>
                <td v-text="pos.autor"></td>
                <td v-text="new Date(pos.created_at).toLocaleDateString('es-ES', {
                  year: 'numeric',
                  month: '2-digit',
                  day: '2-digit',
                  hour: '2-digit',
                  minute: '2-digit',
                  second: '2-digit'
                })"></td>
                <td class="text-center align-middle">
                  <div class="d-flex justify-content-center align-items-center">
                    <router-link :to="{ path: 'viewP/'+ pos.id }" class="btn btn-info btn-sm rounded-circle mx-1">
                      <i class="fa-solid fa-eye"></i>
                    </router-link>
                    <router-link :to="{ path: 'editP/' + pos.id }" class="btn btn-warning btn-sm rounded-circle mx-1">
                      <i class="fa-solid fa-edit"></i>
                    </router-link>
                    <button class="btn btn-danger btn-sm rounded-circle mx-1" v-on:click="eliminar(pos.id, pos.titulo)">
                      <i class="fa-solid fa-trash"></i>
                    </button>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { confirmar } from '../funciones';
export default {
  data() {
    return {
      posts: null,
      cargando: false
    };
  },
  mounted() {
    this.getPosts();
  },
  methods: {
    getPosts() {
      this.cargando = true;
      axios.get('http://127.0.0.1:8000/api/v1/posts').then(res => {
        this.posts = res.data.data;
        this.cargando = false;
      });
    },
    eliminar(id, titulo) {
      confirmar(
        'http://127.0.0.1:8000/api/v1/posts/',
        id,
        'Eliminar Registro',
        'Realmente desea eliminar a ' + titulo + '?',
        this.getPosts
      );
      this.cargando = false;
    }
  }
};
</script>

<style scoped>
.text-truncate {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>

