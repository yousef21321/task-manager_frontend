<template>
  <div class="container">
    <header class="app-header">
      <h1 class="logo">📋 Task Manager</h1>
      <nav class="nav-links">
        <router-link to="/" class="nav-item">Home</router-link>
        <router-link to="/tasks/create" class="btn-primary">+ Add Task</router-link>
      </nav>
    </header>
    
    <main class="main-content">
      <router-view></router-view>
    </main>
  </div>
</template>

<style>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f4f7f6;
  margin: 0;
  color: #333;
}
.container { max-width: 800px; margin: 0 auto; padding: 20px; }
.app-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #e0e0e0; padding-bottom: 15px; margin-bottom: 25px; }
.logo { margin: 0; color: #2c3e50; font-size: 1.8em; }
.nav-links { display: flex; gap: 15px; align-items: center; }
.nav-item { text-decoration: none; color: #3498db; font-weight: bold; }
.btn-primary { background: #2ecc71; color: white; padding: 8px 16px; text-decoration: none; border-radius: 6px; font-weight: bold; border: none; cursor: pointer; }
.card { background: white; padding: 20px; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); margin-bottom: 15px; border: 1px solid #eee; }
</style>