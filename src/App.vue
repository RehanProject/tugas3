<template>
  <!-- Header -->
  <div class="header">
    <h1>To Do List</h1>
  </div>

  <!-- Form untuk membuat baru -->
  <div class="form">
    <input v-model="newTask" type="text" placeholder="Enter new task">
    <button @click="createTask">Create</button>
  </div>

  <!-- Daftar tugas -->
  <div class="tasks">
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task.name }}
        <button @click="editTask(task)">Edit</button>
        <button @click="deleteTask(task)">Delete</button>
      </li>
    </ul>
  </div>

  <!-- Form untuk edit -->
  <div class="form" v-if="editingTask">
    <input v-model="editingTask.name" type="text" placeholder="Enter new task">
    <button @click="updateTask">Update</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      newTask: '',
      editingTask: null
    }
  },
  methods: {
    createTask() {
      if (this.newTask) {
        this.tasks.push({ name: this.newTask, done: false });
        this.newTask = '';
      }
    },
    editTask(task) {
      this.editingTask = task;
    },
    updateTask() {
      this.editingTask = null;
    },
    deleteTask(task) {
      this.tasks = this.tasks.filter(t => t !== task);
    }
  }
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f0f0f0; /* Ubah warna background menjadi warna lain */
  color: #333;
}

.header {
  background-color: #333;
  color: #fff;
  padding: 20px;
  text-align: center;
  border-bottom: 1px solid #333;
}

.header h1 {
  font-size: 24px;
  margin: 0;
  font-weight: bold;
  color: #fff;
}

.form {
  padding: 20px;
  background-color: #333;
  border: 1px solid #333;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.form input[type="text"] {
  width: 100%;
  height: 40px;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #333;
  border-radius: 5px;
}

.form button[type="button"] {
  width: 100%;
  height: 40px;
  padding: 10px;
  font-size: 16px;
  background-color: #333;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.form button[type="button"]:hover {
  background-color: #2ecc71;
}

.tasks {
  padding: 20px;
}

.tasks ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.tasks li {
  padding: 20px;
  border-bottom: 1px solid #333;
}

.tasks li:last-child {
  border-bottom: none;
}

.tasks button[type="button"] {
  margin-left: 10px;
  font-size: 16px;
  background-color: #333;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.tasks button[type="button"]:hover {
  background-color: #2ecc71;
}

.done {
  text-decoration: line-through;
  color: #ccc;
}

.delete {
  color: #e74c3c;
  cursor: pointer;
}

.delete:hover {
  color: #c0392b;
}

/* Responsive Design */
@media only screen and (max-width: 768px) {
  .tasks li {
    padding: 10px;
  }
  .tasks button[type="button"] {
    font-size: 14px;
  }
}

@media only screen and (max-width: 480px) {
  .tasks li {
    padding: 5px;
  }
  .tasks button[type="button"] {
    font-size: 12px;
  }
}
</style>