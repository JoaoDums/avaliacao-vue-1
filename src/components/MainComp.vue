<script setup>
import { ref, computed } from 'vue';
import ListarTarefas from './ListarTarefas.vue';
import AdicionarTarefa from './AdicionarTarefa.vue';

const tarefas = ref([
    { id: 1, descricao: 'Fazer avaliação 1', feita: true },
    { id: 2, descricao: 'Fazer avaliação 2', feita: false },
    { id: 3, descricao: 'Fazer avaliação 3', feita: false },
    { id: 4, descricao: 'Fazer avaliação 4', feita: false },
    { id: 5, descricao: 'Fazer avaliação 5', feita: false },
])
const novaTarefa = ref('');

const tarefasFeitas = computed(() => tarefas.value.filter(tarefa => tarefa.feita).length);

function adicionarTarefa() {
    const lastId = tarefas.value[tarefas.value.length - 1].id;
    tarefas.value.push({ id: lastId + 1, descricao: novaTarefa.value, feita: false });
    novaTarefa.value = '';
}

function finalizarTarefa(id) {
    const index = tarefas.value.findIndex(tarefa => tarefa.id === id);
    tarefas.value[index].feita = true;
}

const turma = 1

const tarefasEmAberto = ref([
    { tarefa: 1, },
    { tarefa: 2, },
    { tarefa: 3, }
])

</script>
<template>

    <section class="container">
        <h1>Avaliação 2 INFO - {{ turma }}</h1>
        <AdicionarTarefa class="card" v-model="novaTarefa" @click="adicionarTarefa" />
        <section class="card tarefas-em-aberto">
            <h2>Tarefas em aberto ({{ tarefasEmAberto }})</h2>
            <ListarTarefas :tarefas="tarefas" @click="finalizarTarefa" />
        </section>

        <section class="card tarefas-feitas">
            <h2>Tarefas feitas ({{ tarefasFeitas }})</h2>
            <ListarTarefas :tarefas="tarefas" realizadas @click="reativarTarefa" />
        </section>
    </section>
</template>
<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.card {
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 10px;
    margin: 10px 0;
    box-shadow: 0 2px 2px 4px rgba(0, 0, 0, 0.1);
    width: 80%;

    &.tarefas-feitas {
        background-color: #d4edda;
    }

    &.tarefas-em-aberto {
        background-color: #f8d7da;
    }
}




.fade2-enter-active,
.fade2-leave-active {
    transition: opacity 0.5s ease-in-out;
}

.fade2-enter-from,
.fade2-leave-to {
    opacity: 0;
}
</style>