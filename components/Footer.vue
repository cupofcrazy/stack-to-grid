<template>
  <footer>
    <p>Stack to Grid Interaction by <a :href="credits.url" target="_blank">{{ credits.label }}</a></p>
  </footer>
</template>

<script setup lang="ts">
const credits = {
  label: 'Tobi',
  url: 'https://x.com/to______bi'
}
</script>

<style scoped>
footer {
  padding: 1rem;
  background: rgba(0, 0, 0, 0.1);
  border-radius: 10rem;
  backdrop-filter: blur(10px);
  font-size: .8rem;
  border: 1px solid rgba(0, 0, 0, 0.1);

  p {
    color: #111;
  }

  a {
    color: blue;
    text-decoration: none;
    font-style: italic;
  }
}
</style>