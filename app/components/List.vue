<script setup lang="ts">
import type { Product } from '~/types/Product';
import Card from '~/components/Card.vue';

defineProps<{
  products: Product[];
}>();
</script>

<template>
  <div class="products-list">
    <Card
      v-for="product in products"
      :key="product.id"
      :product="product"
    />
  </div>
</template>