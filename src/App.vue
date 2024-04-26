<script setup>
import CardList from './components/CardList.vue'
// import TheDrawer from './components/TheDrawer.vue'
import TheHeader from './components/TheHeader.vue'
</script>

<template>
  <!-- <TheDrawer /> -->
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-10">
    <TheHeader />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">All sneakers</h2>

        <div class="flex gap-4">
          <select
            class="px-3 py-2 border rounded-md outline-none focus:border-slate-400 transition"
          >
            <option>By name</option>
            <option>By price(high to low)</option>
            <option>By price(low to high)</option>
          </select>

          <div class="relative">
            <img src="/public/img/search.svg" alt="Search" class="absolute top-3.5 left-4" />
            <input
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-slate-400 transition"
              placeholder="Search"
              type="text"
            />
          </div>
        </div>
      </div>

      <CardList />
    </div>
  </div>
</template>
