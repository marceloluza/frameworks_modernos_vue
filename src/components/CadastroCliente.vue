<script setup lang="ts">
import clienteApi from '@/api/ClienteApi';
import type { ClienteModel } from '@/model/ClienteModel';
import { ref } from 'vue';
import { useRoute } from 'vue-router';

let loading = ref(false);
let successMessage = ref(false);
let errorMessage = ref(false);
let cliente = ref<ClienteModel>({
    id: null,
    nome: '',
    email: '',
    hobbies: ''
})

const route = useRoute()
const id = route?.params?.id;
if (id) {
    clienteApi.buscarPorId(id).then(retorno => {
        console.log(retorno)
        cliente.value = {
            id: retorno.id,
            nome: retorno.nome,
            email: retorno.email,
            hobbies: ''
        }
    });
}


const cadastrar = () => {
    console.log('chamou o cadastrar');
    console.log(cliente);

    loading.value = true;
    clienteApi.salvar(cliente.value).then(retorno => {
        cliente.value = {
            id: null,
            nome: '',
            email: '',
            hobbies: ''
        }
        successMessage.value = true;
        loading.value = false;
    }, error => {
        loading.value = false;
        errorMessage.value = true;
    });
}
</script>
<template>
    <h3>Cadastro de Clientes</h3>
    <div v-if="successMessage" class="alert alert-success" role="alert">
        Cadastro realizado com sucesso.
    </div>
    <div v-if="errorMessage" class="alert alert-danger" role="alert">
        Erro ao realizar o cadastro.
    </div>
    <form @submit.prevent="cadastrar">
        <div class="form-group">
            <label class="form-label">Nome</label>
            <input class="form-control" type="text" v-model="cliente.nome" required />
        </div>
        <div class="form-group">
            <label class="form-label">Email</label>
            <input class="form-control" type="email" v-model="cliente.email" required />
        </div>
        <br>
        <div class="row">
            <div class="col-2">
                <button v-if="!id" class="btn btn-primary" type="submit">Cadastrar</button>
                <button v-if="id" class="btn btn-primary" type="submit">Alterar</button>
            </div>
            <div class="col">
                <div v-if="loading" class="spinner-border" role="status">
                    <span class="sr-only"></span>
                </div>
            </div>
        </div>
    </form>
</template>
<style scoped></style>
