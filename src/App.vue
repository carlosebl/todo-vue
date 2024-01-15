<script setup>
    import { reactive } from 'vue';
    import Cabecalho from './components/Cabecalho.vue';
    import Formulario from './components/Formulario.vue';
    import ListaTarefas from './components/ListaTarefas.vue';

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
        <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
        <Formulario :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value" />
        <ListaTarefas :tarefas="getTarefasFiltradas()" />
    </div>
</template>
