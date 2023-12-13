<script setup >
defineProps({
  image: {
    type: String,
    required: true
  }
})
</script >

<template>
  <div class="flex space-x-4">
    <p class="p-12">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quos
      voluptatibus. Quisquam, quos voluptatibus.
    </p>
    <img :src="image" alt="" class="w-60 h-60">
  </div>
</template>