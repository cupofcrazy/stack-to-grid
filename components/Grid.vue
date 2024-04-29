<template>
  <div class="container" :data-index="collection.id">
    <div class="title">
      <Badge>{{ collection.images.length }} images</Badge>
    </div>

    <div class="grid">
      <div class="grid-item-image" v-for="(image, index) in collection.images" :key="image.id" :data-flip-id="image.id">
        <img :src="image.urls.small_s3" alt="" srcset="" />
      </div>
    </div>
  </div>

</template>

<script setup lang="ts">
import gsap from 'gsap';

const props = defineProps<{
  collection: any
}>()

onMounted(() => {
  gsap.from('.title', {
    opacity: 0,
    y: '-100%',
    delay: .1,
    ease: 'expo.out'
  })
})
</script>

<style scoped>
.title {
  margin-bottom: 2rem;
  text-align: center;
  position: sticky;
  top: 0;
  z-index: 1000;
}

.container {
  --spacing: 2rem;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  padding: var(--spacing);
  overflow-y: auto;
  background: #fff;
  margin: 0 auto;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: var(--spacing);
  width: 100%;
  margin: 0 auto;
  z-index: 10000;
  position: relative;

}

.grid-item-image {
  width: 100%;
  border-radius: 1rem;
  order: -1;
  /* overflow-x: hidden; */
}

img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 1rem;
}
</style>