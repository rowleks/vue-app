<template>
  <div>
    <h5>List rendering</h5>
    <ul>
      <p>Rendering Arrays:</p>
      <li v-for="(fruit, index) in fruits" :key="index">
        {{ fruit }}
      </li>
    </ul>

    <ul>
      <p>Rendering objects:</p>
      <p v-for="(value, key) in person" :key="key">
        <span class="capitalize">{{ key }}:</span> {{ value }}
      </p>
    </ul>
  </div>

  <div>
    <ul class="space-y-2">
      <p>Rendering an array of objects</p>
      <li v-for="(user, index) in users" :key="index">
        <p>Name: {{ user.name }}</p>
        <p>Age: {{ user.age }}</p>
        <p v-if="user.isMember">Member</p>
        <p v-else>Not a member</p>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
const fruits = ["Apple", "Banana", "Cherry", "Date", "Elderberry"];

const person = {
  name: "Rolex",
  age: 30,
  isMember: true,
};

const users = [
  { name: "Alice", age: 25, isMember: true },
  { name: "Bob", age: 28, isMember: false },
  { name: "Charlie", age: 32, isMember: true },
  { name: "Diana", age: 27, isMember: false },
  { name: "Eve", age: 29, isMember: true },
];
</script>

<style scoped>
ul > p:first-child {
  text-decoration: underline;
  text-decoration-skip-ink: none;
}
</style>
