<template>
  <div class="card">
    <h2>{{ isEditing ? '✏️ Edit Task' : '➕ Create New Task' }}</h2>
    <form @submit.prevent="saveTask" class="form-layout">
      
      <div class="input-group">
        <label>Task Title *</label>
        <input v-model="form.title" type="text" required placeholder="Enter task title" class="form-input">
      </div>

      <div class="input-group">
        <label>Description</label>
        <textarea v-model="form.description" rows="4" placeholder="Optional details..." class="form-input"></textarea>
      </div>
      
      <div class="row">
        <div class="input-group half">
          <label>Status</label>
          <select v-model="form.status" class="form-input">
            <option value="pending">Pending</option>
            <option value="in_progress">In Progress</option>
            <option value="done">Done</option>
          </select>
        </div>
        <div class="input-group half">
          <label>Due Date *</label>
          <input v-model="form.due_date" type="date" required class="form-input">
        </div>
      </div>

      <div class="form-actions">
        <button type="submit" :disabled="isSaving" class="btn-primary">
          {{ isSaving ? 'Saving...' : (isEditing ? 'Update Task' : 'Save Task') }}
        </button>
        <button type="button" @click="$router.push('/')" class="btn-cancel">Cancel</button>
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import axios from 'axios'

const route = useRoute()
const router = useRouter()

const isEditing = ref(!!route.params.id)
const isSaving = ref(false)

const form = ref({
  title: '', description: '', status: 'pending', due_date: ''
})

onMounted(async () => {
  if (isEditing.value) {
    try {
      const res = await axios.get(`/api/tasks/${route.params.id}`)
      form.value = res.data
    } catch (error) {
      alert('Task not found!')
      router.push('/')
    }
  }
})

const saveTask = async () => {
  if (!form.value.title || !form.value.due_date) {
    alert('Please fill the required fields!'); return;
  }
  isSaving.value = true
  try {
    if (isEditing.value) { await axios.put(`/api/tasks/${route.params.id}`, form.value) } 
    else { await axios.post('/api/tasks', form.value) }
    router.push('/')
  } catch (error) { alert('An error occurred.') } 
  finally { isSaving.value = false }
}
</script>

<style scoped>
.form-layout { display: flex; flex-direction: column; gap: 15px; }
.input-group { display: flex; flex-direction: column; gap: 5px; }
label { font-weight: bold; font-size: 0.9em; color: #2c3e50; }
.form-input { padding: 10px; border: 1px solid #ccc; border-radius: 6px; font-family: inherit; }
.row { display: flex; gap: 15px; }
.half { flex: 1; }
.form-actions { display: flex; gap: 10px; margin-top: 10px; }
.btn-cancel { background: #95a5a6; color: white; border: none; padding: 10px 15px; border-radius: 6px; cursor: pointer; font-weight: bold; }
</style>