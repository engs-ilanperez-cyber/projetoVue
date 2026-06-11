<template>
  <div class="home">
    <h1>Minha Lista de Tarefas</h1>
    
    <!-- formulário para adicionar tarefas -->
    <TaskForm @adicionar-tarefa="adicionarTarefa" />
    
    <!-- filtros -->
    <div class="filtros">
      <button 
        v-for="filtro in opcoesFiltro" 
        :key="filtro"
        @click="filtroAtivo = filtro"
        :class="{ active: filtroAtivo === filtro }"
      >
        {{ filtro }}
      </button>
    </div>
    
    <!-- lista de tarefas -->
    <div v-if="tarefasFiltradas.length > 0" class="tarefas-lista">
      <TaskCard 
        v-for="tarefa in tarefasFiltradas" 
        :key="tarefa.id"
        :tarefa="tarefa"
        @toggle-tarefa="alternarConcluida"
        @remover-tarefa="removerTarefa"
      />
    </div>
    
    <!-- mensagem quando não há tarefas -->
    <div v-else class="sem-tarefas">
      🎉 Nenhuma tarefa {{ filtroAtivo.toLowerCase() }}!
    </div>
    
    <!-- contador de tarefas -->
    <div class="contador">
      📊 Total: {{ tarefas.length }} | 
      ✅ Concluídas: {{ tarefasConcluidas }} | 
      ⏳ Pendentes: {{ tarefasPendentes }}
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import TaskForm from '@/components/TaskForm.vue'
import TaskCard from '@/components/TaskCard.vue'

// lista de tarefas 
const tarefas = ref([
  { id: 1, titulo: 'Aprender a programar', concluida: false },
  { id: 2, titulo: 'mortal.', concluida: false },
  { id: 3, titulo: 'Reprovar', concluida: false }
])

// filtro ativo
const filtroAtivo = ref('Todas')
const opcoesFiltro = ['Todas', 'Pendentes', 'Concluídas']

// adicionar nova tarefa com id unico
function adicionarTarefa(titulo) {
  const novaTarefa = {
    id: Date.now(),
    titulo: titulo,
    concluida: false
  }
  tarefas.value.push(novaTarefa)
}

// alternar entre concluída/não concluída
function alternarConcluida(id) {
  const tarefa = tarefas.value.find(t => t.id === id)
  if (tarefa) {
    tarefa.concluida = !tarefa.concluida
  }
}

// remover tarefa
function removerTarefa(id) {
  tarefas.value = tarefas.value.filter(t => t.id !== id)
}

// filtro e contadores
const tarefasFiltradas = computed(() => {
  if (filtroAtivo.value === 'Pendentes') {
    return tarefas.value.filter(t => !t.concluida)
  }
  if (filtroAtivo.value === 'Concluídas') {
    return tarefas.value.filter(t => t.concluida)
  }
  return tarefas.value
})

const tarefasConcluidas = computed(() => {
  return tarefas.value.filter(t => t.concluida).length
})

const tarefasPendentes = computed(() => {
  return tarefas.value.filter(t => !t.concluida).length
})
</script>

<style scoped>
.home {
  max-width: 700px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  color: #42b883;
  text-align: center;
  margin-bottom: 30px;
}

/* filtros */
.filtros {
  display: flex;
  gap: 10px;
  justify-content: center;
  margin: 20px 0;
}

.filtros button {
  padding: 8px 16px;
  background-color: #f0f0f0;
  border: 1px solid #ddd;
  border-radius: 20px;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.3s ease;
}

.filtros button:hover {
  background-color: #e0e0e0;
}

.filtros button.active {
  background-color: #42b883;
  color: white;
  border-color: #42b883;
}

/* lista de tarefas */
.tarefas-lista {
  margin: 20px 0;
}

/* mensagem sem tarefas */
.sem-tarefas {
  text-align: center;
  padding: 40px;
  color: #888;
  font-size: 18px;
}

/* contador */
.contador {
  margin-top: 30px;
  padding: 15px;
  background-color: #f5f5f5;
  border-radius: 8px;
  text-align: center;
  font-size: 14px;
  color: #666;
}

/* responsividade */
@media (max-width: 600px) {
  .home {
    padding: 10px;
  }
  
  .filtros {
    gap: 5px;
  }
  
  .filtros button {
    padding: 6px 12px;
    font-size: 12px;
  }
  
  .contador {
    font-size: 12px;
  }
}

/* responsividade para tablet */
@media (min-width: 768px) and (max-width: 1024px) {
  .home {
    max-width: 90%;
  }
  
  .filtros button {
    padding: 8px 20px;
    font-size: 14px;
  }
  
  .task-card {
    padding: 12px;
  }
}

/* responsividade para smartphone */
@media (max-width: 767px) {
  .home {
    padding: 10px;
  }
  
  h1 {
    font-size: 24px;
  }
  
  .form-container {
    padding: 15px;
  }
  
  .input-group {
    flex-direction: column;
    gap: 10px;
  }
  
  input {
    font-size: 16px; 
    padding: 12px;
  }
  
  button {
    padding: 12px;
    font-size: 16px;
  }
  
  .filtros {
    flex-wrap: wrap;
    gap: 8px;
  }
  
  .filtros button {
    padding: 8px 16px;
    font-size: 14px;
    flex: 1;
    min-width: 80px;
  }
  
  .task-card {
    flex-direction: column;
    gap: 10px;
    align-items: flex-start;
  }
  
  .task-content {
    width: 100%;
  }
  
  .delete-btn {
    width: 100%;
    text-align: center;
  }
  
  .contador {
    font-size: 12px;
    padding: 10px;
  }
  
  .sem-tarefas {
    font-size: 14px;
    padding: 30px;
  }
}

/* smartphones pequenos  */
@media (max-width: 480px) {
  .filtros button {
    font-size: 12px;
    padding: 6px 12px;
  }
  
  .task-title {
    font-size: 14px;
  }
  
  .contador {
    display: flex;
    flex-direction: column;
    gap: 5px;
    text-align: center;
  }
}
</style>