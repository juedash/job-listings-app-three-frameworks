<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'active',
      tasks: ['Task One', 'Task Two', 'Task Three', 'Task Four'],
      link: 'https://google.com',
    }
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'pending'
      } else if (this.status === 'pending') {
        this.status = 'inactive'
      } else {
        this.status = 'active'
      }
    },
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
    <a v-bind:href="link" class="text-blue-600">Link to Google</a>
  </div>
</template>
