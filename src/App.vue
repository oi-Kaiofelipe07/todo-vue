<script setup>
import { reactive } from 'vue';

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ tarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <!-- @submit.prevent submit serve oara as atividades serem cadastradas e o prevent para que a pagina não seja atualizada -->
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a classe da tarefa" class="form-control">
        </div>
        <div class="col-md-1">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in filtraTarefas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
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
