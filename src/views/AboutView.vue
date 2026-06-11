<template>
  <div class="about">
    <h1>Sobre o Projeto</h1>
    
    <div class="card">
      <h2>Site de lista de tarefas</h2>
      <p>Este projeto foi desenvolvido como trabalho da disciplina de Desenvolvimento Web, aplicando os conceitos do framework Vue.js. </p>
    </div>

    <div class="card">
      <h2>Funcionalidades Implementadas</h2>
      <ul>
        <li>Adicionar novas tarefas</li>
        <li>Marcar tarefas como concluídas</li>
        <li>Remover tarefas</li>
        <li>Filtrar por status (Todas/Pendentes/Concluídas)</li>
        <li>Contador de tarefas</li>
        <li>Responsividade (funciona em celular/tablet/desktop)</li>
      </ul>
    </div>

    <div class="card">
      <h2>Integrantes</h2>
      <ul>
        <li><strong>Ilan Perez</strong></li>
  
      </ul>
    
    </div>

  </div>
</template>

<style scoped>
.about {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  color: #42b883;
  text-align: center;
  margin-bottom: 30px;
}

.card {
  background-color: #f9f9f9;
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  padding: 20px;
  margin-bottom: 20px;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.card h2 {
  color: #333;
  font-size: 1.3rem;
  margin-top: 0;
  margin-bottom: 15px;
  border-left: 4px solid #42b883;
  padding-left: 12px;
}

.card ul {
  padding-left: 20px;
}

.card li {
  margin: 8px 0;
  color: #555;
}

.tech-badges {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 10px;
}

.badge {
  background-color: #42b883;
  color: white;
  padding: 6px 14px;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 500;
}

.note {
  margin-top: 10px;
  padding: 8px;
  background-color: #fff3cd;
  border-left: 4px solid #ffc107;
  font-size: 0.9rem;
  color: #856404;
}

/* Responsividade */
@media (max-width: 600px) {
  .about {
    padding: 10px;
  }
  
  .card {
    padding: 15px;
  }
  
  .card h2 {
    font-size: 1.1rem;
  }
  
  .badge {
    padding: 4px 10px;
    font-size: 0.8rem;
  }
}
</style>