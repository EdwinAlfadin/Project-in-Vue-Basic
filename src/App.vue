<template>
  <div class="container">
    <Home
      v-if="!winner"
      :participants="participants"
      @add="addParticipant"
      @pick="pickWinner"
    />

    <Winner v-else :winner="winner" @restart="restart" @next="pickWinner" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import Home from "./components/Home.vue";
import Winner from "./components/Winner.vue";

const participants = ref([]);

const remaining = ref([]);

const winner = ref(null);

function addParticipant(name) {
  if (!name.trim()) return;

  participants.value.push(name);

  remaining.value.push(name);
}

function pickWinner() {
  if (remaining.value.length === 0) {
    winner.value = "Semua peserta sudah mendapat giliran";
    return;
  }

  const random = Math.floor(Math.random() * remaining.value.length);

  winner.value = remaining.value[random];

  remaining.value.splice(random, 1);
}

function restart() {
  participants.value = [];

  remaining.value = [];

  winner.value = null;
}
</script>
