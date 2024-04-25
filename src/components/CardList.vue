<script setup>
import ItemCard from './ItemCard.vue'
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <ItemCard
      title="Nike Blazer Mid Suede Men"
      imageUrl="public\img\sneakers\1.jpg"
      :price="89"
      :onClickAdd="false"
      :onClickFavorite="false"
    />
  </div>
</template>
