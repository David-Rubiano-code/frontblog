<template>
    <div class="container mt-5">
    <div class="row align-items-md-stretch ">
      <div class="col-md-6 mt-5">
        <div class="h-100 p-5 text-bg-dark rounded-3">
          <h2>Administrar Post</h2>
          <p>Por medio de este enlace puedes ir a ver los post listados</p>
          <router-link to="viewP" class="btn btn-outline-light" type="button">Ver Post</router-link>
        </div>
      </div>
      <div class="col-md-6 mt-5">
        <div class="h-100 p-5 text-bg-dark rounded-3">
          <h2>Administrar Categorias</h2>
          <p>Por medio de este enlace puedes ir a ver  las Categorias listadas</p>
          <router-link to="viewC" class="btn btn-outline-light" type="button">Ver Categorias</router-link>
        </div>
      </div>
    </div>
    <div class="row align-items-md-stretch ">
      <div class="col-md-6 mt-5">
        <div class="h-100 p-5 text-bg-danger rounded-3">
          <h2>Adevertencia</h2>
          <p>recuerda que todos los cambios que hagas no pueden ser deshechos aqui no existe el CTRL +Z </p>
          
        </div>
      </div>
      <div class="col-md-6 mt-5">
        <div class="h-100 p-5 text-bg-success rounded-3">
          <h2>Exitos</h2>
          <p>
            Esperamos que puedas disfrutar de la aplicacion
            y puedas administrar de manera correcta las cosas

          </p>
        </div>
      </div>
    </div>
  </div>
<div class="container-fluid">
  <router-view/>
</div>
</template>


