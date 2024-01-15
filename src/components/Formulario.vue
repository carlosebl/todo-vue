<script setup>
const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'editaTarefaTemp', 'trocarFiltro']);
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input class="form-control" :value="props.tarefaTemp"
                    @change="props.editaTarefaTemp" required type="text"
                    placeholder="Digite a descrição da tarefa">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="props.trocarFiltro">
                    <option value="Todas">Todas</option>
                    <option value="Pendentes">Pendentes</option>
                    <option value="Finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>