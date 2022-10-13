<script setup lang="ts">
import Paginate from "./components/paginate.vue"
</script>

<template>
  <div>
    <Paginate :totalElement="100" :elementPerPage="10" />
  </div>
</template>

<style scoped></style>
