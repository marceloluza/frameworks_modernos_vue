<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'

</script>
<template>
  <div class="container">
    <nav class="navbar navbar-expand-lg bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Vue Example</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
          aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">              
              <RouterLink class="nav-link active" to="/cadastro-cliente">
                Cadastro Cliente</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink class="nav-link active" to="/lista-cliente">
                Lista de Clientes</RouterLink>
            </li>
            <li class="nav-item">              
              <RouterLink class="nav-link active" to="/cadastro-produto">
                Cadastro Produto</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink class="nav-link active" to="/lista-produto">
                Lista de Produtos</RouterLink>
            </li>              
          </ul>
        </div>
      </div>
    </nav>
    <RouterView />

  </div>
</template>
<style scoped></style>
