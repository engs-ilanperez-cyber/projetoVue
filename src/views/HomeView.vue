<template>
  <div class="home">
    <h1>Minha Lista de Tarefas</h1>
    
    <!-- Formulário para adicionar tarefas -->
    <TaskForm @adicionar-tarefa="adicionarTarefa" />
    
    <!-- Filtros -->
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
    
    <!-- Lista de tarefas -->
    <div v-if="tarefasFiltradas.length > 0" class="tarefas-lista">
      <TaskCard 
        v-for="tarefa in tarefasFiltradas" 
        :key="tarefa.id"
        :tarefa="tarefa"
        @toggle-tarefa="alternarConcluida"
        @remover-tarefa="removerTarefa"
      />
    </div>
    
    <!-- Mensagem quando não há tarefas -->
    <div v-else class="sem-tarefas">
      🎉 Nenhuma tarefa {{ filtroAtivo.toLowerCase() }}!
    </div>
    
    <!-- Contador de tarefas -->
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

// Lista de tarefas (cada tarefa é um objeto)
const tarefas = ref([
  { id: 1, titulo: 'Aprender Vue.js', concluida: false },
  { id: 2, titulo: 'Criar projeto do trabalho', concluida: false },
  { id: 3, titulo: 'Entregar trabalho', concluida: false }
])

// Controle do filtro ativo
const filtroAtivo = ref('Todas')
const opcoesFiltro = ['Todas', 'Pendentes', 'Concluídas']

// Função para adicionar nova tarefa
function adicionarTarefa(titulo) {
  const novaTarefa = {
    id: Date.now(), // ID único baseado no timestamp
    titulo: titulo,
    concluida: false
  }
  tarefas.value.push(novaTarefa)
}

// Função para alternar entre concluída/não concluída
function alternarConcluida(id) {
  const tarefa = tarefas.value.find(t => t.id === id)
  if (tarefa) {
    tarefa.concluida = !tarefa.concluida
  }
}

// Função para remover tarefa
function removerTarefa(id) {
  tarefas.value = tarefas.value.filter(t => t.id !== id)
}

// Propriedades computadas (filtro e contadores)
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

/* Estilo dos filtros */
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

/* Lista de tarefas */
.tarefas-lista {
  margin: 20px 0;
}

/* Mensagem sem tarefas */
.sem-tarefas {
  text-align: center;
  padding: 40px;
  color: #888;
  font-size: 18px;
}

/* Contador */
.contador {
  margin-top: 30px;
  padding: 15px;
  background-color: #f5f5f5;
  border-radius: 8px;
  text-align: center;
  font-size: 14px;
  color: #666;
}

/* Responsividade */
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

/* Responsividade para Tablet (768px - 1024px) */
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

/* Responsividade para Smartphone (até 767px) */
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
    font-size: 16px; /* Evita zoom no iOS */
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

/* Smartphones muito pequenos (até 480px) */
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