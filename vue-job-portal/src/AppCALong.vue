<script>
import { ref } from 'vue'

export default {
  setup() {
    const name = 'John Doe'
    const status = ref('active')
    const tasks = ['Task One', 'Task Two', 'Task Three', 'Task Four']

    const toggleStatus = () => {
      if (status.value === 'active') {
        status.value = 'pending'
      } else if (status.value === 'pending') {
        status.value = 'inactive'
      } else {
        status.value = 'active'
      }
    }

    return {
      name,
      status,
      toggleStatus,
      tasks,
    }
  },
}
</script>

<template>
  <div class="flex flex-col items-center mt-10">
    <h1 class="text-2xl">{{ name }}</h1>
    <p v-if="status === 'active'" class="text-green-600">User is Active</p>
    <p v-else-if="status === 'pending'" class="text-yellow-600">User is Pending</p>
    <p v-else class="text-red-700">User is Inactive</p>
    <button @click="toggleStatus" class="mt-3 px-4 py-2 bg-blue-500 text-white rounded-md">
      Change Status
    </button>
    <h3 class="text-xl my-3">Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task" class="flex items-center my-3">
        {{ task }}
      </li>
    </ul>
  </div>
</template>
