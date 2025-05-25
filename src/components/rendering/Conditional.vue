<template>
  <main>
    <div>
      <h5>Conditional Rendering</h5>
      <p v-if="age >= 18">You are an adult</p>
      <p v-else-if="age > 12 && age < 18">You are a teeneger</p>
      <p v-else="age > 12 && age < 18">You are a child</p>

      <p v-show="show">Works when show equals true</p>
    </div>
    <List />
    <!-- 
    difference between v-show and v-if is v-show simply applies display: none to the element but v-if removes the element from the dom 
    -->
  </main>
</template>

<script setup lang="ts">
import List from "./List.vue";
const age = 20;
const show = false;
</script>

<style scoped></style>
