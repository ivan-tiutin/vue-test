<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    data(): {
        name: string;
        status: 'pending' | 'active' | 'inactive';
        tasks: string[];
        link: string;
    } {
        return {
            name: 'John',
            status: 'pending',
            tasks: ['task1', 'task2', 'task3', 'task4'],
            link: 'https://google.com',
        };
    },
    methods: {
        toggleStatus() {
            if (this.status === 'active') {
                this.status = 'pending';
            } else if (this.status === 'pending') {
                this.status = 'inactive';
            } else {
                this.status = 'active';
            }
        },
    },
});
</script>

<template>
    <h1>{{ name }}</h1>
    <p>User is {{ status }}</p>

    <h1>Tasks:</h1>
    <ul>
        <li v-for="task in tasks" :key="task">{{ task }}</li>
    </ul>
    <!-- <a v-bind:href="link">Click for Google</a> -->
    <a :href="link">Click for Google</a>

    <button @:click="toggleStatus">Change status</button>
</template>

<style scoped></style>
