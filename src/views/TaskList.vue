<template>
  <div>
     <div v-if="isLoading" class="state-msg">⏳ Loading tasks...</div>
    <div v-else-if="filteredTasks.length === 0" class="state-msg">
      🎉 No tasks found.
    </div>
    <div v-else class="task-list">
      <div 
        v-for="task in filteredTasks" 
        :key="task.id" 
        class="card task-item" 
        :class="task.status"
      >
        <div class="task-header">
          <h3>
            <router-link 
              :to="`/tasks/${task.id}`" 
              class="task-title"
            >
              {{ task.title }}
            </router-link>
          </h3>
          <h2>{{task.status}}</h2>
        </div>
        <p class="task-desc">
          {{ task.description || 'No description' }}
        </p>
        <small class="task-meta">
          📅 Due: {{ task.due_date }}
        </small>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import axios from 'axios'
/* ================= STATE ================= */
const tasks = ref([])
const isLoading = ref(true)
const searchQuery = ref('')
const statusFilter = ref('')
const pagination = ref({})

const fetchTasks = async (page = 1) => {
  isLoading.value = true
  try {
    const res = await axios.get('/api/tasks', {
      params: { page }
    })

    tasks.value = res.data.data || res.data
    pagination.value = res.data
  } catch (error) {
    console.error(error)
  } finally {
    isLoading.value = false
  }
}
const filteredTasks = computed(() => {
  return tasks.value.filter(task => {
    const matchesTitle = task.title
      ?.toLowerCase()
      .includes(searchQuery.value.toLowerCase())

    const matchesStatus = statusFilter.value
      ? task.status === statusFilter.value
      : true

    return matchesTitle && matchesStatus
  })
})

onMounted(() => fetchTasks())
</script>

<style scoped>

.state-msg {
  text-align: center;
  padding: 40px;
  color: #7f8c8d;
  font-size: 1.2em;
}

.task-item {
  border-left: 5px solid #ccc;
}

.task-item.pending {
  border-left-color: #e74c3c;
}

.task-item.in_progress {
  border-left-color: #f39c12;
}

.task-item.done {
  border-left-color: #2ecc71;
}

.task-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-title {
  text-decoration: none;
  color: #2c3e50;
}

.status-select {
  padding: 5px;
  border-radius: 4px;
  border: 1px solid #ddd;
}

.task-desc {
  color: #555;
}

.task-meta {
  color: #95a5a6;
}

.task-actions {
  display: flex;
  gap: 10px;
  margin-top: 15px;
}

.btn-sm {
  padding: 6px 12px;
  border-radius: 4px;
  cursor: pointer;
  text-decoration: none;
}

.btn-light {
  background: #ecf0f1;
}

.btn-edit {
  background: #f1c40f;
}

.btn-danger {
  background: #e74c3c;
  color: white;
}

.pagination {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

.btn-page {
  padding: 8px 15px;
  background: #3498db;
  color: white;
  border: none;
}

.btn-page:disabled {
  background: #bdc3c7;
}
</style>