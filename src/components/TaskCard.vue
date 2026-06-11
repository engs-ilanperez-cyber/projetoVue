<template>
  <div class="task-card" :class="{ completed: tarefa.concluida }">
    <div class="task-content">
      <input 
        type="checkbox" 
        :checked="tarefa.concluida"
        @change="$emit('toggle-tarefa', tarefa.id)"
        class="task-checkbox"
      >
      <span class="task-title">{{ tarefa.titulo }}</span>
    </div>
    <div class="task-actions">
      <button @click="$emit('remover-tarefa', tarefa.id)" class="delete-btn">
        Remover
      </button>
    </div>
  </div>
</template>

<script setup>

//recebe os dados da tarefa do componente pai

defineProps({
  tarefa: {
    type: Object,
    required: true
  }
})

//envia eventos para o componente pai

defineEmits(['toggle-tarefa', 'remover-tarefa'])
</script>

<style scoped>

/* formatação */

.task-card {
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s ease;
}

.task-card:hover {
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.task-card.completed {
  background-color: #f0f0f0;
  opacity: 0.7;
}

.task-card.completed .task-title {
  text-decoration: line-through;
  color: #888;
}

.task-content {
  display: flex;
  align-items: center;
  gap: 12px;
  flex: 1;
}

.task-checkbox {
  width: 20px;
  height: 20px;
  cursor: pointer;
}

.task-title {
  font-size: 16px;
  color: #333;
}

.delete-btn {
  padding: 6px 12px;
  background-color: #ff4444;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
}

.delete-btn:hover {
  background-color: #cc0000;
}

/* responsividade */

@media (max-width: 767px) {
  .task-card {
    flex-direction: column;
    align-items: stretch;
    padding: 12px;
  }
  
  .task-content {
    margin-bottom: 8px;
  }
  
  .task-checkbox {
    width: 22px;
    height: 22px;
  }
  
  .delete-btn {
    width: 100%;
    padding: 8px;
  }
}
</style>