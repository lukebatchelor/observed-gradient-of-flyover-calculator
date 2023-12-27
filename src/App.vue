<template>
  <v-app theme="dark">
    <v-main class="mt-2">
      <Main />
    </v-main>
  </v-app>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from "vue";
import Main from "@/components/Main.vue";
</script>
