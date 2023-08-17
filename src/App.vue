<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

const estado = reactive({
  filtro: 'todas',
  tarefaTem: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
    titulo: 'Ir para a academia',
    finalizada: false,
    }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas =() => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
      case 'finalizadas':
      return getTarefasFinalizadas();
      default:
        return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTem,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTem = '';
}

</script>

<template>
<div class="container">
<Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
<Formulario :trocarFiltro="evento => estado.filtro = evento.target.value" :tarefa-tem="estado.tarefaTem" :edita-tarefa-temp="evento => estado.tarefaTem = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
<ListaDeTarefas :tarefas="getTarefasFiltradas()" /> 


</div>
</template>
 

