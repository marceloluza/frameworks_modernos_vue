<script setup lang="ts">
import produtoApi from '@/api/ProdutoApi';
import type { ProdutoModel } from '@/model/ProdutoModel';
import { ref } from 'vue';

const produtos = ref<ProdutoModel[]>([]);
const idExclusao = ref(0);

const listarProdutos = () => {
    produtoApi.listar().then(retorno => {
        produtos.value = retorno;
    });
}
listarProdutos();

const setarIdExclusao = (id) => {
    idExclusao.value = id;
}

const excluir = (id) => {
    console.log('excluir');
    console.log(id);
    produtoApi.excluir(id).then(ret => {
        idExclusao.value = 0;
        listarProdutos();
    });
}

</script>
<template>
    <h3>Lista de Produtos</h3>
    <br>
    <table class="table">
        <thead>
            <tr>
                <th scope="col">ID</th>
                <th scope="col">Nome</th>
                <th scope="col">Categoria</th>
                <th scope="col">Descrição</th>
                <th scope="col">Editar</th>
                <th scope="col">Excluir</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="produto in produtos">
                <td>{{ produto.id }}</td>
                <td>{{ produto.nome }}</td>
                <td>{{ produto.categoria }}</td>
                <td>{{ produto.descricao }}</td>
                <td>
                    <RouterLink class="btn btn-secondary" :to="{ path: 'cadastro-produto/' + produto.id }">
                        Editar</RouterLink>
                </td>
                <td>
                    <button @click="setarIdExclusao(produto.id)" type="button" class="btn btn-danger" data-bs-toggle="modal"
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
