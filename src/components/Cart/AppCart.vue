<script setup lang="ts">
import type { ProductCartInterface } from '@/interfaces'
import { computed } from 'vue'
import AppCartProductList from './AppCartProductList.vue'

const props = defineProps<{
  cart: ProductCartInterface[]
}>()

const totalPrice = computed(() =>
  props.cart.reduce((acc, product) => {
    return acc + product.price * product.quantity
  }, 0),
)

const emit = defineEmits<{
  (e: 'removeProductFromCart', productId: number): void
}>()
</script>

<template>
  <div class="p-20 d-flex flex-column">
    <h2 class="mb-10">Panier</h2>
    <AppCartProductList
      class="flex-fill"
      :cart="cart"
      @remove-product-from-cart="emit('removeProductFromCart', $event)"
    />
    <button class="btn btn-success">Commander ({{ totalPrice }}€)</button>
  </div>
</template>

<style lang="scss" scoped></style>
