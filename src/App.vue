<script setup>
import ItemCard from './components/ItemCard.vue'
import TheHeader from './components/TheHeader.vue'
</script>

<template>
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-10">
    <TheHeader />

    <div>
      <ItemCard />
      <ItemCard />
      <ItemCard />
    </div>
  </div>
</template>
