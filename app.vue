<template>
  <div>
    <h1>HOLA {{ mundo }}</h1>
    <p>{{ cafes }}</p>
  </div>
</template>
<script setup lang="ts">
let mundo = '---';

const search = ref('');
const page = ref(1);

const getCafes = async () => {
  console.log('Geting cafés');
};
await getCafes();
const { data: cafes, error } = await useAsyncData(
  'cafes',
  () =>
    $fetch(`/api/v1/cafes`, {
      method: 'GET',
      baseURL: 'https://api.roastandbrew.coffee',
      params: {
        page: page.value,
        search: search.value,
      },
    }),
  {
    watch: [page, search],
  }
);
</script>
