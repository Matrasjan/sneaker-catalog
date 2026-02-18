<script setup lang="ts">
import { useProductsStore } from '~/stores/products';
import { useProducts } from '~/composables/useProducts';
import List from '~/components/List.vue';

const store = useProductsStore();
const { fetchProducts } = useProducts();
const { fetchNextPage } = store;

if (store.products.length === 0) {
  const { data, error } = await useAsyncData('products', () =>
    fetchProducts(1, store.limit),
  );

  if (data.value) {
    store.setInitialData(data.value);
  }

  if (error.value) {
    store.error = true;
  }
}

const loadMore = async (): Promise<void> => {
  await fetchNextPage();
};
</script>

<template>
  <section class="catalog">
    <h1 class="catalog__title">каталог</h1>

    <div class="catalog__container">
      <List :products="store.products" />

      <div class="catalog__controls">
        <div
          v-if="store.loading"
          class="catalog__loading"
        >
          Загрузка...
        </div>

        <div
          v-if="store.error"
          class="catalog__error"
        >
          <p class="catalog__error-text">
            Произошла ошибка, попробуйте позже
          </p>
          <button
            class="catalog__retry"
            @click="store.retry"
          >
            Повторить
          </button>
        </div>

        <button
          v-if="store.hasNextPage && !store.loading && !store.error"
          class="catalog__more"
          @click="loadMore"
        >
          Показать ещё
        </button>
      </div>
    </div>
  </section>
</template>
