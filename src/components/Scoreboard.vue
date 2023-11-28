<script setup>
import { ref, reactive, onMounted } from 'vue';

let data = ref([{
    "team": "Cercle Brugge",
    "score": "26"
},
{
    "team": "KAA Gent",
    "score": "28"
}]);

let socket = null;

onMounted( () => {
    socket = new WebSocket('wss://labo6-1fcb.onrender.com/primus');

    //listen for new data
    socket.onmessage = function (event) {
        let m = JSON.parse(event.data);
        console.log(m);
        if (m.action === 'updateStats') {
            data.value.push({
                "team": m.team,
                "score": m.score
            });
        }
    };
});
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