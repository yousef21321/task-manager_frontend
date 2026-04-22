<template>
  <div v-if="task" class="card">
    <div class="detail-header">
      <h2>{{ task.title }}</h2>
      <span class="badge">{{ task.status.replace('_', ' ').toUpperCase() }}</span>
    </div>
    
    <div class="detail-body">
      <h4>Description:</h4>
      <p>{{ task.description || 'No description provided.' }}</p>
    </div>

    <div class="detail-meta">
      <p><strong>📅 Due Date:</strong> {{ task.due_date }}</p>
      <p><strong>⏱️ Created:</strong> {{ new Date(task.created_at).toLocaleDateString() }}</p>
    </div>

    <div class="detail-actions">
      <button @click="$router.push('/')" class="btn-cancel">&larr; Back</button>
    </div>
  </div>
  <div v-else class="state-msg">⏳ Loading Details...</div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'

const route = useRoute()
const task = ref(null)
onMounted(async () => {
  try {
    const res = await axios.get(`/api/tasks/${route.params.id}`)
    task.value = res.data.data    

  } catch (error) { alert('Task not found') }
})
</script>

<style scoped>
.detail-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #eee; padding-bottom: 15px; margin-bottom: 15px; }
.detail-header h2 { margin: 0; color: #2c3e50; }
.badge { background: #34495e; color: white; padding: 5px 12px; border-radius: 12px; font-size: 0.85em; }
.detail-body p { font-size: 1.1em; line-height: 1.6; color: #444; }
.detail-meta { background: #f9f9f9; padding: 15px; border-radius: 6px; margin: 20px 0; border: 1px solid #eee; }
.detail-meta p { margin: 5px 0; color: #555; }
.detail-actions { display: flex; gap: 10px; }
.btn-cancel { background: #bdc3c7; border: none; padding: 10px 15px; border-radius: 6px; cursor: pointer; font-weight: bold; color: #333; }
.btn-edit { background: #f1c40f; border: none; padding: 10px 15px; border-radius: 6px; cursor: pointer; font-weight: bold; color: #333; }
.state-msg { text-align: center; padding: 40px; font-size: 1.2em; color: #7f8c8d; }
</style>