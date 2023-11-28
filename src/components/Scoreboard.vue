<script setup>
import { ref, reactive, onMounted } from 'vue';

let data = reactive([{
    "team": "Cercle Brugge",
    "score": "26"
},
{
    "team": "KAA Gent",
    "score": "28"
}]);
</script>

<template>
    <h1>Scoreboard</h1>
    <ul>
        <li v-for="item in data" :key="item.team">
            {{ item.team }}: {{ item.score }}
        </li>
    </ul>
</template>
  
<style scoped></style>