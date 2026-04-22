<template>
  <div class="filters-bar">
    <input 
      :value="searchQuery"
      @input="$emit('update:searchQuery', $event.target.value)"
      type="text" 
      placeholder="Search by title..." 
      class="form-input search-input"
    />

<select 
  :value="statusFilter"
  @change="$emit('update:statusFilter', $event.target.value)"
  class="form-input"
>
  <option value="">All Status</option>
  <option value="pending">Pending</option>
  <option value="in_progress">In Progress</option>
  <option value="done">Done</option>
</select>
  </div>
</template>

<script setup>
defineProps({
  searchQuery: String,
  statusFilter: String
})
defineEmits(['update:searchQuery', 'update:statusFilter'])
</script>
<style scoped>

.filters-bar {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.form-input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
}

.search-input {
  flex: 2;
}

</style>