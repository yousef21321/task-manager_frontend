# 📝 Task Manager (Vue 3 + Laravel API)

A simple task management application built with **Vue 3 (Composition API)** and connected to a backend API (Laravel).

---

## 🚀 Features

* 📋 Display tasks list
* 🔍 Search tasks by title
* 🏷️ Filter tasks by status (Pending / In Progress / Done)
* ✏️ Edit task
* ❌ Delete task
* 🔄 Update task status مباشرة من القائمة
* 📄 Pagination
* 🧩 Reusable Filters Component

---

## 🧱 Project Structure

```
src/
│
├── components/
│   └── TaskFilters.vue   # Filters component (search + status)
│
├── views/
│   └── TaskDetail.vue
│   └── TaskForm.vue       
│   └── TaskList.vue       

│
├── router/
│   └── index.js
│

```

---

## ⚙️ Installation

```bash
npm install
```

---

## ▶️ Run Project

```bash
npm run dev
```

---

## 🔗 API Endpoints

| Method | Endpoint        | Description        |
| ------ | --------------- | ------------------ |
| GET    | /api/tasks      | Get all tasks      |
| PUT    | /api/tasks/{id} | Update task status |
| DELETE | /api/tasks/{id} | Delete task        |

---

## 🧩 Filters Component Usage

```vue
<TaskFilters
  v-model:searchQuery="searchQuery"
  v-model:statusFilter="statusFilter"
/>
```

s
## 🎨 UI Behavior

* لون الكارت بيتغير حسب الحالة:

  * 🔴 Pending
  * 🟡 In Progress
  * 🟢 Done

---

## 💡 Future Improvements

* 🔍 Debounce search input
* 🌐 Server-side filtering
* 📅 Filter by due date
* ⚡ تحسين الأداء باستخدام caching
* 🔐 Authentication & Authorization

---

## 👨‍💻 Author

Youssef Abdou

---

## 📄 License

This project is open-source and available for learning purposes.
