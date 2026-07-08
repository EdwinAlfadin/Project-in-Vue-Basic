<template>

<div class="winner">

<h2>The winner is :</h2>

<h1>{{ winner }}</h1>

<button @click="$emit('restart')">
Start Over
</button>

<button
class="secondary"
@click="$emit('next')"
>
Want a new winner?
</button>

</div>

</template>

<script setup>

defineProps({
winner:String
})

defineEmits([
"restart",
"next"
])

</script>