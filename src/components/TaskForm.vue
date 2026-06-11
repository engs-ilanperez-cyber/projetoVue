<template>
  <div class="form-container">
    <h3>Adicionar Nova Tarefa</h3>
    <div class="input-group">
      <input 
        type="text" 
        v-model="novaTarefa"
        @keyup.enter="adicionarTarefa"
        placeholder="Digite sua tarefa..."
      >
      <button @click="adicionarTarefa">
        ➕ Adicionar
     </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

//variável para armazenar o texto da tarefa
const novaTarefa = ref('')

// função para adicionar uma tarefa
function adicionarTarefa() {
  if (novaTarefa.value.trim() !== '') {
    // emite um evento para o componente pai
    emit('adicionar-tarefa', novaTarefa.value)
    // limpa o input
    novaTarefa.value = ''
  }
}

// define qual evento este componente pode emitir
const emit = defineEmits(['adicionar-tarefa'])
</script>

<style scoped>

/* formatação */

.form-container {
  background-color: #f5f5f5;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
}

h3 {
  margin: 0 0 15px 0;
  color: #333;
}

.input-group {
  display: flex;
  gap: 10px;
}

input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
}

button {
  padding: 10px 20px;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #359268;
}
</style>