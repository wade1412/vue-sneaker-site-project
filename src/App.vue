<script setup>
import CardList from './components/CardList.vue'
import TheDrawer from './components/TheDrawer.vue'
import TheHeader from './components/TheHeader.vue'
</script>

<template>
  <TheDrawer />
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-10">
    <TheHeader />

    <div class="p-10">
      <h2 class="text-3xl font-bold mb-8">All sneakers</h2>

      <CardList />
    </div>
  </div>
</template>
