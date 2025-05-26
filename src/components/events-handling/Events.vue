<template>
  <main>
    <div>
      <h2>{{ count }}</h2>
      <div>
        <button :disabled="count < 1" @click="decrement">-1</button>
        <button v-on:click="reset">Reset</button>
        <button @click="increment">+1</button>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from "vue";

const count = ref(0);

function increment() {
  count.value++;
}
function decrement() {
  count.value--;
}
function reset() {
  count.value = 0;
}

// Handle keyboard events for incrementing, decrementing, and resetting the count

function handleKeydown(e: KeyboardEvent) {
  if (e.ctrlKey && e.key === "ArrowRight") {
    increment();
  } else if (e.ctrlKey && e.key === "ArrowLeft") {
    if (count.value > 0) {
      decrement();
    }
  } else if (e.key === "Escape") {
    reset();
  }
}

// Add event listeners for keydown events when the component is mounted and remove them when it is unmounted
onMounted(() => {
  window.addEventListener("keydown", handleKeydown);
});

onBeforeUnmount(() => {
  window.removeEventListener("keydown", handleKeydown);
});
</script>

<style scoped>
@reference "tailwindcss";
button {
  @apply bg-blue-500 text-white px-4 py-2 rounded cursor-pointer disabled:bg-gray-300;
}

h2 {
  @apply text-7xl font-bold text-center mb-4;
  color: #333;
}

h2 ~ div {
  @apply flex gap-2 justify-center items-center;
}
</style>
