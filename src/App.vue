<script setup>
import { onMounted, provide, reactive, ref, watch } from 'vue'
import CardList from './components/CardList.vue'
import TheDrawer from './components/TheDrawer.vue'
import TheHeader from './components/TheHeader.vue'
import axios from 'axios'

const items = ref([])

const drawerOpen = ref(false)

const openDrawer = () => {
  drawerOpen.value = true
}

const closeDrawer = () => {
  drawerOpen.value = false
}

const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}

const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      const obj = {
        parentId: item.id
      }
      item.isFavorite = true

      const { data } = await axios.post(`https://0e6425652546c825.mokky.dev/favorites`, obj)

      item.favoriteId = data.id
    } else {
      await axios.delete(`https://0e6425652546c825.mokky.dev/favorites/${item.favoriteId}`)
      item.favoriteId = null
    }
  } catch (err) {
    console.log(err)
  }
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(`https://0e6425652546c825.mokky.dev/favorites`)

    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.parentId === item.id)

      if (!favorite) {
        return item
      }

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    })
  } catch (err) {
    console.log(err)
  }
}
const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get(`https://0e6425652546c825.mokky.dev/items`, { params })

    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      isAdded: false,
      favoriteId: null
    }))
  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavorites()
})

watch(filters, fetchItems)

provide('cartActions', {
  closeDrawer,
  openDrawer
})
</script>

<template>
  <TheDrawer v-if="drawerOpen" />
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-10">
    <TheHeader @open-drawer="openDrawer" />

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
              @input="onChangeSearchInput"
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-slate-400 transition"
              placeholder="Search"
              type="text"
            />
          </div>
        </div>
      </div>

      <div class="mt-10">
        <CardList :items="items" @add-to-favorite="addToFavorite" />
      </div>
    </div>
  </div>
</template>
