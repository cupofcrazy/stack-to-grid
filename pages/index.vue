<template>
  <div class="gallery">
    <div class="stacks" :style="{ opacity: selectedCollection ? 0 : 1 }">
      <button class="stack-item" @click="handleClick(collection)" v-for="(collection, index) in filteredCollections"
        :data-index="collection.id">
        <Stack :key="index" :collection="collection" />
        <Badge>Collection #{{ index + 1 }}</Badge>
      </button>

    </div>
    <Grid v-if="selectedCollection" :collection="selectedCollection" @click="handleChange(selectedCollection.id)" />
  </div>
</template>

<script setup lang="ts">
import { gsap } from 'gsap';
import { Flip } from 'gsap/Flip';

gsap.registerPlugin(Flip);

const baseURL = 'https://api.unsplash.com'
const { data: collections } = await useAsyncData<any>('collections', async () => {
  const cols = await Promise.all([
    $fetch(`${baseURL}/collections/1971015/photos?client_id=${process.env.UNSPLASH_ACCESS_KEY}`),
    $fetch(`${baseURL}/collections/8337454/photos?client_id=${process.env.UNSPLASH_ACCESS_KEY}`),
    $fetch(`${baseURL}/collections/WM2WLKriadU/photos?client_id=${process.env.UNSPLASH_ACCESS_KEY}`),
    $fetch(`${baseURL}/collections/1961725/photos?client_id=${process.env.UNSPLASH_ACCESS_KEY}`),
    $fetch(`${baseURL}/collections/3485552/photos?client_id=${process.env.UNSPLASH_ACCESS_KEY}`),
    $fetch(`${baseURL}/collections/1755999/photos?client_id=${process.env.UNSPLASH_ACCESS_KEY}`),

  ])
  console.log({ cols })


  return {
    data: cols
  }
})
const filteredCollections = computed(() => collections.value.data.reduce((acc: any, collection: any, index: any) => {
  acc.push({
    images: collection,
    id: index
  })
  return acc
}, []))

const selectedCollection = ref<any>(null)

const handleClick = (collection: any) => {
  selectedCollection.value = collection
  const state = Flip.getState('.stack-item-image, .grid-item-image')

  nextTick(() => {
    Flip.from(state, {
      targets: '.grid-item-image',
      duration: .8,
      absolute: true,
      ease: 'elastic.out(.7, .7)',
      stagger: -0.01
    })
  })
}

const handleChange = (index: number) => {
  selectedCollection.value = null
  const state = Flip.getState('.stack-item-image, .grid-item-image')

  nextTick(() => {
    gsap.set(`.stack-item[data-index="${index}"]`, {
      zIndex: 10000
    })
    Flip.from(state, {
      targets: '.stack-item-image',
      duration: 1,
      absolute: true,
      ease: 'elastic.out(.7, .7)',
      stagger: 0.01,
      onComplete: () => {
        gsap.set(`.stack-item[data-index="${index}"]`, {
          clearProps: 'z-index'
        })
      }
    })
  })
}
</script>

<style lang="css" scoped>
@keyframes shimmerEffect {
  from {
    background-position-x: 100%;
    opacity: 1;
  }

  to {
    background-position-x: 0%;
    opacity: 0;
  }
}

.gallery {
  --width: 960px;
  padding: 1rem;
  max-width: var(--width);
  margin: 0 auto;
  user-select: none;
}

.stack-item {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  align-items: center;
  justify-content: center;
  padding: 5rem;
  /* height: calc(var(--width) / 3.5); */
  transition: all 0.3s ease;
  border-radius: 1rem;
  background: none;
  border: none;
}

.stack-item:hover {
  cursor: pointer;
  background: rgba(0, 0, 0, 0.05);
  transition: all 0.3s ease;
}

.stack-item:hover:deep(.images) {
  transform: scale(1.1);
  transition: all 0.3s ease;
}

.stack-item:hover:deep(.images::after) {
  opacity: 1;
  animation: shimmerEffect .3s ease-out;
}

.stacks {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 2fr));
  gap: 1rem;
}
</style>