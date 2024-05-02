<script setup>
import CartHead from './CartHead.vue'
import CartItemList from './CartItemList.vue'

defineProps({
  totalPrice: Number,
  vatPrice: Number
})
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-50"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <CartHead />

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
        disabled=""
        class="bg-blue-200 w-full rounded-xl py-3 text-xl font-bold text-white hover:bg-blue-300 transition active:bg-lime-500 disabled:bg-slate-300 cursor-pointer"
      >
        Confirm order
      </button>
    </div>
  </div>
</template>
