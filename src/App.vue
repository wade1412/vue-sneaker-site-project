<script setup>
import { onMounted, reactive, ref, watch } from 'vue'
import CardList from './components/CardList.vue'
// import TheDrawer from './components/TheDrawer.vue'
import TheHeader from './components/TheHeader.vue'
import axios from 'axios'

const items = ref([])

const filters = reactive({
  sortBy: '',
  searchQuery: ''
})

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

onMounted(async () => {
  try {
    const { data } = await axios.get('https://0e6425652546c825.mokky.dev/items')

    items.value = data
  } catch (err) {
    console.log(err)
  }
})

watch(filters, async () => {
  try {
    const { data } = await axios.get('https://0e6425652546c825.mokky.dev/items' + filters.sortBy)

    items.value = data
  } catch (err) {
    console.log(err)
  }
})
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
            @change="onChangeSelect"
          >
            <option value="name">By name</option>
            <option value="price">By price(high to low)</option>
            <option value="-pice">By price(low to high)</option>
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

      <div class="mt-10">
        <CardList :items="items" />
      </div>
    </div>
  </div>
</template>
