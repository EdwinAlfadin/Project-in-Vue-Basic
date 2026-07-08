<template>
  <div>
    <h1>Who Can Get Arisan</h1>

    <div class="input-area">
      <input v-model="name" placeholder="Masukkan Nama" />

      <button @click="add">Add</button>
    </div>

    <div class="list">
      <span v-for="person in participants" :key="person" class="badge">
        {{ person }}
      </span>
    </div>

    <button
      class="winner-btn"
      @click="$emit('pick')"
      :disabled="participants.length == 0"
    >
      Check The Winner
    </button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  participants: Array,
});
const emit = defineEmits(["add", "pick"]);
const name = ref("");

function add() {
  const newName = name.value.trim();

  if (!newName) return;

  const isExist = props.participants.some(
    (item) => item.toLowerCase() === newName.toLowerCase(),
  );

  if (isExist) {
    alert("Nama sudah ada!");
    return;
  }

  emit("add", newName);
  name.value = "";
}
</script>
