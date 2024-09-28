<script setup lang="ts">
import clienteApi from '@/api/ClienteApi';
import type { ClienteModel } from '@/model/ClienteModel';
import { ref } from 'vue';

const clientes = ref<ClienteModel[]>([]);
const idExclusao = ref(0);

const listarClientes = () => {
    clienteApi.listar().then(retorno => {
        clientes.value = retorno;
    });
}
listarClientes();

const setarIdExclusao = (id) => {
    idExclusao.value = id;
}

const excluir = (id) => {
    console.log('excluir');
    console.log(id);
    clienteApi.excluir(id).then(ret => {
        idExclusao.value = 0;
        listarClientes();
    });
}

</script>
<template>
    <h3>Lista de Clientes</h3>
    <br>
    <table class="table">
        <thead>
            <tr>
                <th scope="col">ID</th>
                <th scope="col">Nome</th>
                <th scope="col">Email</th>
                <th scope="col">Editar</th>
                <th scope="col">Excluir</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="cliente in clientes">
                <td>{{ cliente.id }}</td>
                <td>{{ cliente.nome }}</td>
                <td>{{ cliente.email }}</td>
                <td>
                    <RouterLink class="btn btn-secondary" :to="{ path: 'cadastro-cliente/' + cliente.id }">
                        Editar</RouterLink>
                </td>
                <td>
                    <button @click="setarIdExclusao(cliente.id)" type="button" class="btn btn-danger" data-bs-toggle="modal"
                        data-bs-target="#modalExcluir">
                        Excluir
                    </button>
                </td>
            </tr>
        </tbody>
    </table>

    <div class="modal fade" id="modalExcluir" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h1 class="modal-title fs-5" id="exampleModalLabel">Confirmação</h1>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    Deseja realmente excluir?
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
                    <button @click="excluir(idExclusao)" data-bs-dismiss="modal" type="button"
                        class="btn btn-primary">Confirmar</button>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped></style>
