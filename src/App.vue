<script setup>
    import { reactive } from 'vue';

    const estado = reactive({
        filtro: 'Todas',
        tarefaTemp: '',
        tarefas: [
            {
                titulo: 'Estudar ES6',
                finalizada: false
            },
            {
                titulo: 'Estudar SASS',
                finalizada: false
            },
            {
                titulo: 'Treino',
                finalizada: true
            }
        ]
    })

    const getTarefasPendentes = () => {
        return estado.tarefas.filter(tarefa => !tarefa.finalizada);
    }

    const getTarefasFinalizadas = () => {
        return estado.tarefas.filter(tarefa => tarefa.finalizada);
    }

    const getTarefasFiltradas = () => {
        const{ filtro }= estado;

        switch (filtro) {
            case 'Pendentes':
                return getTarefasPendentes();
            case 'Finalizadas':
                return getTarefasFinalizadas();
            default:
                return estado.tarefas;
        }
    }

    const cadastraTarefa = () => {
        const novaTarefa = {
            titulo: estado.tarefaTemp,
            finalizada: false
        }
        estado.tarefas.push(novaTarefa);
        estado.tarefaTemp = '';
    }
</script>

<template>
<div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <p>
            Você possui {{ getTarefasPendentes().length }} tarefas pendentes
        </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
        <div class="row">
            <div class="col">
                <input class="form-control" :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite a descrição da tarefa">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="evento => estado.filtro = evento.target.value">
                    <option value="Todas">Todas</option>
                    <option value="Pendentes">Pendentes</option>
                    <option value="Finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
            <label class="ms-3" :class="{ done: tarefa.finalizada }" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</div>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>
