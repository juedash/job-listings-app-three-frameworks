<script setup>
import { onMounted, ref } from 'vue'
const name = 'John Doe'
const status = ref('active')
const tasks = ref(['Task One', 'Task Two', 'Task Three', 'Task Four'])
const newTask = ref('')

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()
    tasks.value = data.map((item) => item.title)
  } catch (error) {
    console.log('Error fetching tasks')
  }
})

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending'
  } else if (status.value === 'pending') {
    status.value = 'inactive'
  } else {
    status.value = 'active'
  }
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask)
    newTask.value = ''
  }
}
const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}
</script>

<template>
  <div class="flex flex-col items-center mt-10">
    <h1 class="text-2xl">{{ name }}</h1>
    <p v-if="status === 'active'" class="text-green-600">User is Active</p>
    <p v-else-if="status === 'pending'" class="text-yellow-600">User is Pending</p>
    <p v-else class="text-red-700">User is Inactive</p>
    <form @submit.prevent="addTask">
      <label for="newTask">Add Task</label>
      <input type="text" id="newTask" v-model="newTask" />
      <button type="submit">Submit</button>
    </form>

    <h3 class="text-xl my-3">Tasks:</h3>
    <ul>
      <li v-for="(task, index) in tasks" :key="task" class="flex items-center my-3">
        <span>
          {{ task }}
        </span>
        <button @click="deleteTask(index)">x</button>
      </li>
    </ul>
    <button @click="toggleStatus" class="mt-3 px-4 py-2 bg-blue-500 text-white rounded-md">
      Change Status
    </button>
  </div>
</template>
