<script setup lang="ts">
import { computed, ref } from "vue"

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

let selectedPage = ref(1)
let firstPageCount = ref(1)
let lastPageCount = ref(1)
let middlePageCountStart = ref(0)
let middlePageCountEnd = ref(0)

const totalPageCount = computed(() => {
  return Math.ceil(props.totalElement / props.elementPerPage)
})

const getPaginationList = () => {
  if (totalPageCount.value > 4) {
    firstPageCount.value = 3
    lastPageCount.value = 4
  } else {
    firstPageCount.value = totalPageCount.value
    lastPageCount.value = totalPageCount.value + 1
  }

  if (totalPageCount.value - 1 > 4)
    lastPageCount.value = totalPageCount.value - 1

  if (
    selectedPage.value > firstPageCount.value &&
    selectedPage.value < lastPageCount.value
  ) {
    firstPageCount.value = 1
    lastPageCount.value = totalPageCount.value
    middlePageCountStart.value =
      selectedPage.value > 1 ? selectedPage.value - 1 : selectedPage.value
    middlePageCountEnd.value =
      selectedPage.value < totalPageCount.value
        ? selectedPage.value + 1
        : selectedPage.value
  } else {
    middlePageCountStart.value = -1
    middlePageCountEnd.value = -2
  }

  console.log(
    "first page count ",
    firstPageCount.value,
    "last page count ",
    lastPageCount.value
  )
}
getPaginationList()

const onPageSelect = (pageNo: number) => {
  if (pageNo > totalPageCount.value || pageNo < 1) return
  selectedPage.value = pageNo
  getPaginationList()
}

const range = (start: number, end: number) => {
  return Array(end - start + 1)
    .fill()
    .map((_, idx) => start + idx)
}
</script>

<template>
  <ul :class="$style.list">
    <li @click="onPageSelect(1)">
      <img src="../assets/double-arrow-left.svg" alt="" width="15" />
    </li>
    <li @click="onPageSelect(selectedPage - 1)">
      <img src="../assets/arrow-left.svg" alt="" width="15" />
    </li>
    <li
      v-for="pageNo in firstPageCount"
      :key="pageNo"
      :class="pageNo == selectedPage ? $style.selected_page : ''"
      @click="onPageSelect(pageNo)"
    >
      {{ pageNo }}
    </li>
    <li v-show="middlePageCountStart + 1 > 1">...</li>
    <li
      v-for="pageNo in range(middlePageCountStart, middlePageCountEnd)"
      :key="pageNo"
      :class="pageNo == selectedPage ? $style.selected_page : ''"
      @click="onPageSelect(pageNo)"
    >
      {{ pageNo }}
    </li>
    <li
      v-show="
        totalPageCount > firstPageCount + 2 &&
        middlePageCountEnd + 1 < totalPageCount
      "
    >
      ...
    </li>
    <li
      v-for="pageNo in range(lastPageCount, totalPageCount)"
      :key="pageNo"
      :class="pageNo == selectedPage ? $style.selected_page : ''"
      @click="onPageSelect(pageNo)"
    >
      {{ pageNo }}
    </li>

    <li @click="onPageSelect(selectedPage + 1)">
      <img src="../assets/arrow-right.svg" alt="" width="15" />
    </li>
    <li @click="onPageSelect(totalPageCount)">
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

.list li:hover,
.selected_page {
  background-color: #0096ff;
  color: white;
}
</style>
