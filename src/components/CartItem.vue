<script setup>
defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  price: Number
})
</script>

<template>
  <div class="flex items-center border border-slate-100 p-4 rounded-xl gap-4">
    <img :src="imageUrl" alt="Sneaker" class="w-16 h-16" />

    <div class="flex flex-col flex-1">
      <p>{{ title }}</p>

      <div class="flex justify-between mt-2 flex-1">
        <b> {{ price }} </b>
        <img
          class="opacity-50 hover:opacity-100 cursor-pointer transition"
          src="/public/img/btn-remove.svg"
          alt="Remove"
        />
      </div>
    </div>
  </div>
</template>
