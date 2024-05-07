<script setup>
import CartHead from './CartHead.vue'
import CartItemList from './CartItemList.vue'
import EmptyCartInfo from './EmptyCartInfo.vue'

const emit = defineEmits(['createOrder'])

defineProps({
  totalPrice: Number,
  vatPrice: Number,
  isCartButtonDisabled: Boolean
})
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-50"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <CartHead />

    <div v-if="!totalPrice" class="flex h-full items-center">
      <EmptyCartInfo
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
          @click="() => emit('createOrder')"
        >
          Confirm order
        </button>
      </div>
    </div>
  </div>
</template>
