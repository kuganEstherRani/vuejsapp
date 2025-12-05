<template>
  <div class="container">
    <!-- Create / Update Form -->
    <form @submit.prevent="saveUser" class="form">
      <h2>{{ isEditing ? "Update User" : "Add User" }}</h2>

      <input v-model="form.name" placeholder="Enter name" required />
      <input v-model="form.email" placeholder="Enter email" required />

      <button type="submit">
        {{ isEditing ? "Update" : "Add" }}
      </button>

      <button v-if="isEditing" type="button" @click="cancelEdit" class="cancel-btn">
        Cancel
      </button>
    </form>

    <!-- User Table -->
    <h2>User List</h2>
    <table class="table">
      <thead>
        <tr>
          <th>#</th>
          <th>Name</th>
          <th>Email</th>
          <th>Actions</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(user, index) in users" :key="user.id">
          <td>{{ index + 1 }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>
            <button class="edit-btn" @click="editUser(user)">Edit</button>
            <button class="delete-btn" @click="deleteUser(user.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>

    <p v-if="users.length === 0">No users yet.</p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const users = ref([
  { id: 1, name: "John Doe", email: "john@gmail.com" },
]);

const form = ref({ id: null, name: "", email: "" });
const isEditing = ref(false);

// Create or Update
function saveUser() {
  if (isEditing.value) {
    // Update
    const index = users.value.findIndex(u => u.id === form.value.id);
    users.value[index] = { ...form.value };
    isEditing.value = false;
  } else {
    // Create
    users.value.push({
      id: Date.now(),
      name: form.value.name,
      email: form.value.email,
    });
  }

  resetForm();
}

// Delete
function deleteUser(id) {
  users.value = users.value.filter(u => u.id !== id);
}

// Edit
function editUser(user) {
  form.value = { ...user };
  isEditing.value = true;
}

function cancelEdit() {
  resetForm();
  isEditing.value = false;
}

function resetForm() {
  form.value = { id: null, name: "", email: "" };
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: auto;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 30px;
}

input {
  padding: 10px;
  border: 1px solid #ccc;
}

button {
  padding: 10px;
  background: #42b883;
  border: none;
  color: white;
  cursor: pointer;
}

.cancel-btn {
  background: #999;
}

.edit-btn {
  background: #3498db;
  margin-right: 5px;
}

.delete-btn {
  background: #e74c3c;
}

.table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.table th,
.table td {
  padding: 10px;
  border-bottom: 1px solid #ccc;
}
</style>
