<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import Lista from './components/Lista.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefa: [
    {
      titulo:'Estudar Java',
      finalizada: false,
    },
    {
      titulo:'Estudar Java',
      finalizada: false,
    },
    {
      titulo:'Estudar Java',
      finalizada: false,
    },
  ]
})

const tarefasPendentes = () => {
  return estado.tarefa.filter(tarefa => !tarefa.finalizada)
}

const tarefasFinalizadas = () => {
  return estado.tarefa.filter(tarefa => tarefa.finalizada)
}

const filtraTarefas = () => {
  const {filtro} = estado

  switch (filtro) {
    case 'pendentes':
      return tarefasPendentes();
    case 'finalizadas':
      return tarefasFinalizadas();
    default:
      return estado.tarefa;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefa.push(tarefaNova);
  estado.tarefaTemp = '';
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="tarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarrefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <Lista :tarefas="filtraTarefas()" />
  </div>
</template>
