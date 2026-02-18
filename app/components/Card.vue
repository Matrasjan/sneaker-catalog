<script setup lang="ts">
import type { Product } from '~/types/Product';

const props = defineProps<{
  product: Product;
}>();
</script>

<template>
  <a href="#" class="product-card">
    <div class="product-card__image-wrapper">
      <img
        src="/image.png"
        :alt="product.name"
        class="product-card__image"
      />

      <img src="/favorite.png" class="favorite" alt="Добавить в избранное" />
    </div>

    <div class="product-card__content">
      <div class="product-card__prices">
        <span class="product-card__price">16 285 ₽</span>

        <span class="product-card__price--half">8 328 ₽ x2</span>
      </div>

      <div class="product-card__title">Adidas Originals Gazelle</div>
    </div>
  </a>
</template>
