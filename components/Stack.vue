<template>
  <div class="images" :data-index="collection.id">
    <div class="stack-item-image" v-for="(image, index) in collection.images" :key="image.id"
      :style="{ zIndex: collection.images.length + index }" :data-flip-id="image.id">
      <img :src="image.urls.small_s3" alt="" srcset="" />
    </div>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{
  collection: any
}>()
</script>

<style lang="css" scoped>
.images {
  position: relative;
  display: flex;
  width: 100px;
  height: 100px;
  margin-top: 2rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.images::after {
  opacity: 0;
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(-45deg, rgba(255, 255, 255, 0) 40%, rgba(255, 255, 255, .75) 50%, rgba(255, 255, 255, 0) 60%);
  background-size: 300%;
  background-position-x: 120%;
  z-index: 100;
  /* transition: all 0.5s; */
}

.images:hover:after {}

.stack-item-image {
  width: 100px;
  height: 100px;
  background-color: white;
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  border-radius: 1rem;
  position: absolute;
  overflow: hidden;
}

img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.stack-item-image:nth-of-type(1n) {
  transform: rotate(5deg);
}

.stack-item-image:nth-of-type(2n) {
  transform: rotate(-5deg);
}

.stack-item-image:nth-of-type(3n) {
  transform: rotate(10deg);
}
</style>