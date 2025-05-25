<script setup lang="ts">
import image1 from "../assets/vue-green-bg.jpg";
import image2 from "../assets/vue-white-bg.jpg";

const isRed = true; // bind condition for class

const imgData = {
  src: image1,
  alt: "vue.js logo",
};
const imgData2 = {
  src: image2,
  alt: "vue.js logo",
};

const { src, alt } = imgData;
</script>

<template>
  <!-- class binding -->
  <main class="space-y-10">
    <div>
      <p>class binding</p>
      <h1 class="box" :class="isRed && 'red-box'">Direct method</h1>

      <h2 class="box" :class="{ 'red-box-2': isRed }">Object method</h2>

      <h3 class="box" :class="[isRed && 'red-box-3']">Array method</h3>
    </div>

    <!-- src/alt binding -->
    <div>
      <p>src/alt binding</p>
      <img :src="src" :alt="alt" />
      <!-- 
      If the attribute has the same name as the variable name of the JavaScript value being bound, the syntax can be further shortened to omit the attribute value for instance <img :src :alt /> 
      -->

      <!-- 
      You can pass an object to v-bind to bind multiple attributes like the example below
      -->
      <img v-bind="imgData2" />
    </div>
  </main>
</template>

<style scoped>
@reference "tailwindcss";
main > * {
  @apply space-y-2;
}

img {
  @apply object-contain block w-full aspect-video;
}

.red-box {
  @apply bg-red-300 text-white;
}

.red-box-2 {
  @apply bg-red-500 text-white;
}

.red-box-3 {
  @apply bg-red-700 text-white;
}

.box {
  @apply p-2.5 border-1 border-[#ccc];
}
</style>
