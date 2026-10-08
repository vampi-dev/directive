<script setup>
import { ref } from 'vue'
import users from './users.json'

const username = ref('')
const password = ref('')
const role = ref('')
const loggedIn = ref(false)

function login() {
  if (
    users[username.value] &&
    users[username.value].password === password.value
  ) {
    loggedIn.value = true
    role.value = users[username.value].role
  } else {
    loggedIn.value = false
    role.value = ''
    alert("Invalid username or password")
  }
}

function logout() {
  loggedIn.value = false
  username.value = ''
  password.value = ''
  role.value = ''
}
</script>

<template>
  <div class="container">

  
    <div v-if="!loggedIn">
      <h1>Role Based Login</h1>

    
      <input
        v-model="username"
        placeholder="Username"
      />

      <input
        v-model="password"
        type="password"
        placeholder="Password"
      />

      
      <button v-on:click="login">
        Login
      </button>
    </div>

    <div v-else>
      <h1>Welcome {{ username }}</h1>

      <h2>Role: {{ role }}</h2>

      <p v-show="role === 'Admin'">
        You can manage all users.
      </p>

      <p v-show="role === 'User'">
        You can view your dashboard.
      </p>

      <p v-show="role === 'Guest'">
        You have limited access.
      </p>

      <h3>Available Roles:</h3>

      <ul>
        <li v-for="user in users" :key="user.role">
          {{ user.role }}
        </li>
      </ul>

      <button v-on:click="logout">
        Logout
      </button>
    </div>

  </div>
</template>

<style>
.container {
  width: 400px;
  margin: 100px auto;
  padding: 30px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 10px;
}

input {
  display: block;
  width: 90%;
  padding: 10px;
  margin: 10px auto;
}

button {
  padding: 10px 20px;
  margin: 10px;
  cursor: pointer;
}
</style>