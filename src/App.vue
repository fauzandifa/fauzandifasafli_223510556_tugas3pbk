<template>
  <div class="container mt-5">
    <h1>aplikasi simpel to do list</h1>
    <h3>silahkan masukkan apa yg ingin kamu lakukan</h3>
    <img src="/src/assets/WhatsApp Image 2024-05-15 at 09.28.49.jpeg" alt="" height="150px" width="150px">
    <!-- Form untuk menambahkan tugas baru -->
    <div class="input-group mb-3">
      <input type="text" v-model="newTodo" class="form-control" placeholder="Add a new task..." />
      <div class="input-group-append">
        <button @click="addTodo" class="btn btn-primary">Add</button>
      </div>
    </div>

    <!-- Daftar tugas -->
    <ul class="list-group">
      <li
        class="list-group-item d-flex justify-content-between align-items-center"
        v-for="(todo, index) in todos"
        :key="todo.id"
      >
        <!-- Tampilkan teks tugas -->
        <div class="todo-text" @click="toggleEdit(todo)" v-if="!todo.editing">{{ todo.text }}</div>
        <!-- Tampilkan form edit jika sedang dalam mode edit -->
        <input
          v-else
          type="text"
          v-model="todo.text"
          @keyup.enter="updateTodo(todo)"
          class="form-control"
        />
        <!-- Tombol untuk menghapus tugas -->
        <button @click="removeTodo(todo.id)" class="btn btn-danger btn-sm">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
      nextTodoId: 1
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ id: this.nextTodoId++, text: this.newTodo, editing: false })
        this.newTodo = '' // Reset input
      }
    },
    removeTodo(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId)
    },
    toggleEdit(todo) {
      todo.editing = true
    },
    updateTodo(todo) {
      todo.editing = false
    }
  }
}
</script>

<style>
/* CSS styling */
html, body {
  height: 100%;
  margin: 0;
  font-family: Arial, sans-serif;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url(https://i.pinimg.com/564x/be/8c/c9/be8cc91ca24dea985ec394dfd8e5ff74.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.container {
  max-width: 600px;
  width: 100%; /* Ensure the container takes up full width up to max-width */
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1, h3 {
  text-align: center;
  color: #343a40;
}

.input-group {
  margin-bottom: 1rem;
}

.input-group .form-control {
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
}

.input-group .btn-primary {
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
}

.list-group-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 15px;
  margin-bottom: 5px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.todo-text {
  flex: 1;
  cursor: pointer;
  padding-right: 10px;
}

.todo-text:hover {
  text-decoration: underline;
}

.list-group-item input.form-control {
  margin-right: 10px;
}

.btn-danger {
  border-radius: 4px;
}

img {
  display: block;
  margin: 0 auto 20px; /* Center the image and add some space below it */
}
</style>
