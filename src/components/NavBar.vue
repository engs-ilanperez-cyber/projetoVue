<template>
  <nav class="navbar">
    <div class="nav-container">
      <div class="logo">
        <span>✅ TaskManager</span>
      </div>
      <div class="nav-links">
        <router-link to="/" class="nav-link" active-class="active-link" exact-active-class="active-link">
          🏠 Home
        </router-link>
        <router-link to="/about" class="nav-link" active-class="active-link">
          ℹ️ Sobre
        </router-link>
      </div>
    </div>
  </nav>
</template>

<script setup>
// Não precisa de lógica adicional
</script>

<style scoped>
.navbar {
  background-color: #2c3e50;
  color: white;
  padding: 1rem 0;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

.logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: #42b883;
}

.nav-links {
  display: flex;
  gap: 20px;
}

.nav-link {
  color: white;
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 8px;
  transition: all 0.3s ease;
  font-size: 1rem;
}

.nav-link:hover {
  background-color: #42b883;
  color: white;
}

.active-link {
  background-color: #42b883;
  color: white;
}

/* Responsividade */
@media (max-width: 600px) {
  .nav-container {
    flex-direction: column;
    gap: 10px;
  }
  
  .logo {
    font-size: 1.2rem;
  }
  
  .nav-link {
    padding: 6px 12px;
    font-size: 0.9rem;
  }
}
</style>