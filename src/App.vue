<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    data() {
        return {
            name: 'John',
            status: 'pending',
            tasks: ['task1', 'task2', 'task3', 'task4'],
        }
    },
})
</script>

<template>
    <h1>{{ name }}</h1>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User in inactive</p>

    <h1>Tasks:</h1>
    <ul>
        <li v-for="task in tasks" :key="task">{{ task }}</li>
    </ul>
</template>

<style scoped></style>
