<script setup>
import { computed, provide, ref, watch } from 'vue'
import TheDrawer from './components/TheDrawer.vue'
import TheHeader from './components/TheHeader.vue'
import axios from 'axios'

// Cart logic
const cart = ref([])
const isCreatingOrder = ref(false)

const drawerOpen = ref(false)

const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))
const vatPrice = computed(() => Math.round(totalPrice.value * 5) / 100)

const cartIsEmpty = computed(() => cart.value.length === 0)
const isCartButtonDisabled = computed(() => isCreatingOrder.value || cartIsEmpty.value)

const openDrawer = () => {
  drawerOpen.value = true
}

const closeDrawer = () => {
  drawerOpen.value = false
}

const addToCart = (item) => {
  cart.value.push(item)
  item.isAdded = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)
  item.isAdded = false
}

const createOrder = async () => {
  try {
    isCreatingOrder.value = true
    const { data } = await axios.post(`https://0e6425652546c825.mokky.dev/orders`, {
      items: cart.value,
      totalPrice: totalPrice.value + vatPrice.value
    })

    cart.value = []

    return data
  } catch (err) {
    console.log(err)
  } finally {
    isCreatingOrder.value = false
  }
}

watch(
  cart,
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  {
    deep: true
  }
)

provide('cart', {
  cart,
  closeDrawer,
  openDrawer,
  addToCart,
  removeFromCart
})
// Cart logic
</script>

<template>
  <TheDrawer
    v-if="drawerOpen"
    :total-price="totalPrice"
    :vat-price="vatPrice"
    @create-order="createOrder"
    :is-cart-button-disabled="isCartButtonDisabled"
  />
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-10">
    <TheHeader @open-drawer="openDrawer" :total-price="totalPrice" />

    <div class="p-10">
      <router-view></router-view>
    </div>
  </div>
</template>
