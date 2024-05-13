<script setup>
import { computed, inject, ref } from 'vue'
import axios from 'axios'
import CartHead from './CartHead.vue'
import CartItemList from './CartItemList.vue'
import CartInfoBlock from './CartInfoBlock.vue'

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number
})

const { cart } = inject('cart')

const isCreatingOrder = ref(false)
const orderId = ref(null)

const createOrder = async () => {
  try {
    isCreatingOrder.value = true
    const { data } = await axios.post(`https://0e6425652546c825.mokky.dev/orders`, {
      items: cart.value,
      totalPrice: props.totalPrice.value + props.vatPrice.value
    })

    cart.value = []

    orderId.value = data.id
    return data
  } catch (err) {
    console.log(err)
  } finally {
    isCreatingOrder.value = false
  }
}

const cartIsEmpty = computed(() => cart.value.length === 0)

const isCartButtonDisabled = computed(() => isCreatingOrder.value || cartIsEmpty.value)
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-50"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <CartHead />

    <div v-if="!totalPrice || orderId" class="flex h-full items-center">
      <CartInfoBlock
        v-if="orderId"
        title="Your order has been placed"
        :description="`Order #${orderId} will be delivered to you soon!`"
        imageUrl="/public/img/complete-order.jpg"
      />
      <CartInfoBlock
        v-if="!totalPrice && !orderId"
        title="Your cart is empty"
        description="Go pick yourself a nice pair to make an order!"
        imageUrl="/public/img/empty-cart.jpg"
      />
    </div>

    <div v-else>
      <CartItemList />

      <div class="flex flex-col gap-4 my-7 bottom-0 content-evenly">
        <div class="flex gap-2">
          <span> Total:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>${{ totalPrice }}</b>
        </div>

        <div class="flex gap-2">
          <span> Tax:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>${{ vatPrice }}</b>
        </div>
        <button
          :disabled="isCartButtonDisabled"
          class="bg-blue-300 w-full rounded-xl py-3 text-xl font-bold text-white hover:bg-blue-400 transition active:bg-blue-500 disabled:bg-slate-300 cursor-pointer"
          @click="createOrder"
        >
          Confirm order
        </button>
      </div>
    </div>
  </div>
</template>
