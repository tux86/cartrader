<script setup>

import useFetchCars from "~/composables/useFetchCars";

const route=useRoute()
const {data:cars, refresh} = await useFetchCars(route.params.city, {
  minPrice: route.query.minPrice,
  maxPrice: route.query.maxPrice,
  make: route.params.make
})

watch(()=> route.query, ()=> {
  window.location.reload() // not best practice due to bug in lib
});

</script>

<template>
  <div>
    <CarCards v-if="cars.length" :cars="cars" />
    <div v-else>
      <h1 class="text-red-600">No Cars Found With Filters</h1>
    </div>
  </div>
</template>
