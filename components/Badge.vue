<template>
  <span class="badge">
    <slot />
  </span>
</template>

<script setup lang="ts">

</script>

<style scoped>
.badge {
  --gradient-bg: linear-gradient(180deg, rgba(255, 255, 255, 0.70) 0%, rgba(217, 217, 217, 0.7) 50%, rgba(255, 255, 255, 0.70) 100%);
  color: rgba(0, 0, 0, .8);
  font-size: 1rem;
  padding: .25rem .5rem;
  border: 1px solid rgba(0, 0, 0, .1);
  border-radius: 10rem;
  background: var(--gradient-bg);
  box-shadow: 0 2px 4px rgba(0, 0, 0, .1);
}
</style>