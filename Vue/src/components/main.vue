<template>
  <ul>
    <li v-for="item in talks.dialogue" :key="item.id">
      <div class="dialogue">
        <div class="request">{{ item.request }}</div>
        <div class="response">{{ item.response }}</div>
      </div>
    </li>
  </ul>
</template>

<script  setup>
import { defineProps } from "vue";
const props = defineProps(["talks"]);
</script>

<style scoped>
</style>
