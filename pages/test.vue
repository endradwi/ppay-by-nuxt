<script setup>
import { ref } from 'vue'

const counter = useState('counter', () => 0) 
const sameCounter = useState('counter')

const nameInput = ref('') // State untuk input
const nameList = ref([]) // Array penyimpanan nama
const inputType = ref('password') // Default: input sebagai password

const submitForm = () => {
  if (nameInput.value.trim() !== '') {
    nameList.value.push(nameInput.value)
    nameInput.value = ''
  }
}

// Fungsi untuk toggle input antara "password" dan "text"
const togglePassword = () => {
  inputType.value = inputType.value === 'password' ? 'text' : 'password'
}
</script>

<template>
  <p>Counter: {{ counter }}</p>
  <div class="flex gap-2 my-4">
    <UButton @click="counter--"> - </UButton>
    <button @click="counter++"> + </button>
  </div>
  <p>Same Counter: {{ sameCounter }}</p>

  <form @submit.prevent="submitForm">
    <label for="name">Password:</label>
    <input v-model="nameInput" :type="inputType" style="background-color: yellow;">
    <button type="button" @click="togglePassword">
      {{ inputType === 'password' ? 'Show' : 'Hide' }}
    </button>
    <button style="background-color: aqua;">Submit</button>
  </form>

  <table border="1" style="margin-top: 10px;">
    <thead>
      <tr>
        <th>Password (Hidden)</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(name, index) in nameList" :key="index">
        <td>•••••••</td> <!-- Menampilkan dalam format tersembunyi -->
      </tr>
    </tbody>
  </table>
</template>
