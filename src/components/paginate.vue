<script setup lang="ts">
import { computed } from "vue"

const props = defineProps({
  totalElement: {
    type: Number,
    default: 1,
  },
  elementPerPage: {
    type: Number,
    default: 1,
  },
})

const totalPageCount = computed(() => {
  return Math.ceil(props.totalElement / props.elementPerPage)
})
</script>

<template>
  <ul :class="$style.list">
    <li>
      <img src="../assets/double-arrow-left.svg" alt="" width="15" />
    </li>
    <li>
      <img src="../assets/arrow-left.svg" alt="" width="15" />
    </li>
    <li>
      {{ totalPageCount }}
    </li>

    <li>
      <img src="../assets/arrow-right.svg" alt="" width="15" />
    </li>
    <li>
      <img src="../assets/double-arrow-right.svg" alt="" width="15" />
    </li>
  </ul>
</template>

<style module>
.list {
  list-style: none;
  display: flex;
}

.list li {
  border-left: 1px solid black;
  border-top: 1px solid black;
  border-bottom: 1px solid black;
  min-width: 23px;
  height: 27px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-left: 5px;
  padding-right: 5px;
  cursor: pointer;
}

.list li:first-child {
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
  border-right: none;
}

.list li:last-child {
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  border-right: 1px solid black;
}

.list li:hover {
  background-color: #0096ff;
}
</style>
