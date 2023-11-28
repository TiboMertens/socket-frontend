<script setup>
import { ref, reactive, onMounted } from 'vue';
let teams = reactive(["Anderlecht", "Antwerp", "OHL"]);
let selectedTeam = ref(null);

let score = ref(null);

let socket = null;

onMounted(() => {
    socket = new WebSocket('ws://localhost:3000/primus');
});

const updateStats = () => {
    let m = {
        "action": "updateStats",
        "team": selectedTeam.value,
        "score": score.value
    };

    socket.send(JSON.stringify(m));
};

</script>

<template>
    <h1>Update stats</h1>
    <label for="teamSelect">Select Team:</label>
    <select v-model="selectedTeam" id="teamSelect">
      <option v-for="team in teams" :key="team" :value="team">{{ team }}</option>
    </select>
    <input type="text" v-model="score">
    <button @click="updateStats">Update</button>
    
</template>
  
<style scoped></style>