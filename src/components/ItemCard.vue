<script setup>
defineProps({
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean
})
</script>

<template>
  <div
    class="relative bg-white border border-slate-100 rounded-xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition"
  >
    <img
      src="D:\React Projects\vue-sneaker-site-project\public\img\liked.svg"
      alt="Like 1"
      class="absolute top-8 left-8"
    />
    <img :src="imageUrl" alt="Sneaker" />
    <p class="mt-2">{{ title }}</p>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Price:</span>
        <span>${{ price }}</span>
      </div>

      <img src="D:\React Projects\vue-sneaker-site-project\public\img\plus.svg" alt="AddToCart" />
    </div>
  </div>
</template>
