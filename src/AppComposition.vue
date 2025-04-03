<script setup lang="ts">
import { onMounted, ref } from 'vue';

const name = ref('Ivan');
const status = ref('active');
const tasks = ref(['task1', 'task10', 'task3', 'task4']);
const newTask = ref('');

const toggleStatus = () => {
    if (status.value === 'active') {
        status.value = 'pending';
    } else if (status.value === 'pending') {
        status.value = 'inactive';
    } else {
        status.value = 'active';
    }
};

const addTask = () => {
    if (newTask.value.trim() !== '') {
        tasks.value.push(newTask.value);
        newTask.value = '';
    }
};

const deleteTask = (index: number) => {
    tasks.value.splice(index, 1);
};

onMounted(async () => {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos');
        const data = await response.json();
        if (response.status === 200) {
            tasks.value = data.map((task: { title: string }) => task.title);
        } else {
            alert('Something went wrong');
        }
    } catch (error) {
        alert(error);
    }
});
</script>

<template>
    <h1>{{ name }}</h1>
    <p>User is {{ status }}</p>

    <form @submit.prevent="addTask">
        <label for="newTask">Task name</label>
        <input type="text" id="newTask" name="newTask" v-model="newTask" />
        <button type="submit">Submit</button>
    </form>

    <h3>Tasks:</h3>
    <ul>
        <li v-for="(task, index) in tasks" :key="task">
            <span>{{ task }}</span>
            <button @:click="deleteTask(index)">Delete</button>
        </li>
    </ul>

    <button @:click="toggleStatus">Change status</button>
</template>

<style scoped></style>
