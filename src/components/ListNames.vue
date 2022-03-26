<template>
  <div>
    <ul>
      <li :key="names.id" v-for="names in names">
        {{ names.Name }} {{ names.Price }} kr
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ListNames",

  props: {
    names: Object,
  },
};
</script>

<style></style>
