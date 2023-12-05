<script setup>
import Playground from './components/Playground.vue';
</script>

<template>
  <div class="m-5">
    <Playground :isRequired="false" />
    <Playground :isRequired="true" />
  </div>
</template>
