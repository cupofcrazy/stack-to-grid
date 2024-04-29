<template>
  <span class="badge" :style="{ backgroundColor: color }">
    <slot>Badge</slot>
  </span>
</template>

<script setup lang="ts">
type Props = {
  color: string
}
withDefaults(defineProps<Props>(), ({
  color: '#fff'
}))
</script>

<style scoped>
.badge {
  color: rgba(0, 0, 0, .7);
  font-size: .8rem;
  padding: .4rem .6rem;
  border-radius: 10rem;
  border: 1px solid rgba(0, 0, 0, .1);
}
</style>