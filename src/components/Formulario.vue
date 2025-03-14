<script setup>
    const props = defineProps(['cadastraTarefa', 'tarrefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <!-- @submit.prevent submit serve oara as atividades serem cadastradas e o prevent para que a pagina não seja atualizada -->
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarrefaTemp" @change="props.editaTarefaTemp" required
                    type="text" placeholder="Digite aqui a classe da tarefa" class="form-control">
            </div>
            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>