<template>
  <v-app theme="dark">
    <v-main class="mt-2">
      <Main />
    </v-main>
  </v-app>
</template>

<style scoped>
@font-face {
  font-family: "Handwriting";
  src: url("GloriaHallelujah-Regular.ttf");
}
</style>

<script setup lang="ts">
import { ref, computed, onMounted } from "vue";
import Main from "@/components/Main.vue";
</script>
