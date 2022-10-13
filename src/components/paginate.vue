<script setup lang="ts">
import { computed, ref } from "vue";

const props = defineProps({
  totalElement: {
    type: Number,
    default: 1,
  },
  elementPerPage: {
    type: Number,
    default: 1,
  },
});
const emit = defineEmits(["onPageClick"]);

let selectedPage = ref(1);
let firstPageCount = ref(1);
let lastPageCount = ref(1);
let middlePageCountStart = ref(0);
let middlePageCountEnd = ref(0);

const totalPageCount = computed(() => {
  return Math.ceil(props.totalElement / props.elementPerPage);
});

const getPaginationList = () => {
  if (totalPageCount.value > 4) {
    firstPageCount.value = 3;
    lastPageCount.value = 4;
  } else {
    firstPageCount.value = totalPageCount.value;
    lastPageCount.value = totalPageCount.value + 1;
  }

  if (totalPageCount.value - 1 > 4)
    lastPageCount.value = totalPageCount.value - 1;

  if (
    selectedPage.value > firstPageCount.value &&
    selectedPage.value < lastPageCount.value
  ) {
    firstPageCount.value = 1;
    lastPageCount.value = totalPageCount.value;
    middlePageCountStart.value =
      selectedPage.value > 1 ? selectedPage.value - 1 : selectedPage.value;
    middlePageCountEnd.value =
      selectedPage.value < totalPageCount.value
        ? selectedPage.value + 1
        : selectedPage.value;
  } else {
    middlePageCountStart.value = -1;
    middlePageCountEnd.value = -2;
  }
};
getPaginationList();

const onPageSelect = (pageNo: number) => {
  if (pageNo > totalPageCount.value || pageNo < 1) return;
  selectedPage.value = pageNo;
  getPaginationList();
  emit("onPageClick", pageNo);
};

const range = (start: number, end: number) => {
  return Array(end - start + 1)
    .fill(undefined)
    .map((_, idx) => start + idx);
};
</script>

<template>
  <ul :class="$style.list">
    <li @click="onPageSelect(1)">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        version="1.1"
        width="15"
        height="15"
        viewBox="0 0 256 256"
        xml:space="preserve"
      >
        <defs></defs>
        <g
          style="
            stroke: none;
            stroke-width: 0;
            stroke-dasharray: none;
            stroke-linecap: butt;
            stroke-linejoin: miter;
            stroke-miterlimit: 10;
            fill: none;
            fill-rule: nonzero;
            opacity: 1;
          "
          transform="translate(1.4065934065934016 1.4065934065934016) scale(2.81 2.81)"
        >
          <path
            d="M 80.521 90 c 0.768 0 1.536 -0.293 2.121 -0.879 c 1.172 -1.171 1.172 -3.071 0 -4.242 L 42.763 45 L 82.643 5.121 c 1.172 -1.171 1.172 -3.071 0 -4.242 c -1.171 -1.172 -3.071 -1.172 -4.242 0 l -42 42 c -0.563 0.563 -0.879 1.325 -0.879 2.121 s 0.316 1.559 0.879 2.121 l 42 42 C 78.986 89.707 79.754 90 80.521 90 z"
            style="
              stroke: none;
              stroke-width: 1;
              stroke-dasharray: none;
              stroke-linecap: butt;
              stroke-linejoin: miter;
              stroke-miterlimit: 10;
              fill: rgb(0, 0, 0);
              fill-rule: nonzero;
              opacity: 1;
            "
            transform=" matrix(1 0 0 1 0 0) "
            stroke-linecap="round"
          />
          <path
            d="M 51.478 90 c 0.768 0 1.536 -0.293 2.121 -0.879 c 1.172 -1.171 1.172 -3.071 0 -4.242 L 13.72 45 L 53.599 5.121 c 1.172 -1.171 1.172 -3.071 0 -4.242 c -1.171 -1.172 -3.072 -1.171 -4.242 0 l -42 42 c -1.172 1.171 -1.172 3.071 0 4.242 l 42 42 C 49.942 89.707 50.71 90 51.478 90 z"
            style="
              stroke: none;
              stroke-width: 1;
              stroke-dasharray: none;
              stroke-linecap: butt;
              stroke-linejoin: miter;
              stroke-miterlimit: 10;
              fill: rgb(0, 0, 0);
              fill-rule: nonzero;
              opacity: 1;
            "
            transform=" matrix(1 0 0 1 0 0) "
            stroke-linecap="round"
          />
        </g>
      </svg>
    </li>
    <li @click="onPageSelect(selectedPage - 1)">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        version="1.1"
        width="15"
        height="15"
        viewBox="0 0 256 256"
        xml:space="preserve"
      >
        <defs></defs>
        <g
          style="
            stroke: none;
            stroke-width: 0;
            stroke-dasharray: none;
            stroke-linecap: butt;
            stroke-linejoin: miter;
            stroke-miterlimit: 10;
            fill: none;
            fill-rule: nonzero;
            opacity: 1;
          "
          transform="translate(1.4065934065934016 1.4065934065934016) scale(2.81 2.81)"
        >
          <path
            d="M 65.75 90 c 0.896 0 1.792 -0.342 2.475 -1.025 c 1.367 -1.366 1.367 -3.583 0 -4.949 L 29.2 45 L 68.225 5.975 c 1.367 -1.367 1.367 -3.583 0 -4.95 c -1.367 -1.366 -3.583 -1.366 -4.95 0 l -41.5 41.5 c -1.367 1.366 -1.367 3.583 0 4.949 l 41.5 41.5 C 63.958 89.658 64.854 90 65.75 90 z"
            style="
              stroke: none;
              stroke-width: 1;
              stroke-dasharray: none;
              stroke-linecap: butt;
              stroke-linejoin: miter;
              stroke-miterlimit: 10;
              fill: rgb(0, 0, 0);
              fill-rule: nonzero;
              opacity: 1;
            "
            transform=" matrix(1 0 0 1 0 0) "
            stroke-linecap="round"
          />
        </g>
      </svg>
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
      <svg
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        version="1.1"
        width="15"
        height="15"
        viewBox="0 0 256 256"
        xml:space="preserve"
      >
        <defs></defs>
        <g
          style="
            stroke: none;
            stroke-width: 0;
            stroke-dasharray: none;
            stroke-linecap: butt;
            stroke-linejoin: miter;
            stroke-miterlimit: 10;
            fill: none;
            fill-rule: nonzero;
            opacity: 1;
          "
          transform="translate(1.4065934065934016 1.4065934065934016) scale(2.81 2.81)"
        >
          <path
            d="M 24.25 90 c -0.896 0 -1.792 -0.342 -2.475 -1.025 c -1.367 -1.366 -1.367 -3.583 0 -4.949 L 60.8 45 L 21.775 5.975 c -1.367 -1.367 -1.367 -3.583 0 -4.95 c 1.367 -1.366 3.583 -1.366 4.95 0 l 41.5 41.5 c 1.367 1.366 1.367 3.583 0 4.949 l -41.5 41.5 C 26.042 89.658 25.146 90 24.25 90 z"
            style="
              stroke: none;
              stroke-width: 1;
              stroke-dasharray: none;
              stroke-linecap: butt;
              stroke-linejoin: miter;
              stroke-miterlimit: 10;
              fill: rgb(0, 0, 0);
              fill-rule: nonzero;
              opacity: 1;
            "
            transform=" matrix(1 0 0 1 0 0) "
            stroke-linecap="round"
          />
        </g>
      </svg>
    </li>
    <li @click="onPageSelect(totalPageCount)">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        version="1.1"
        width="15"
        height="15"
        viewBox="0 0 256 256"
        xml:space="preserve"
      >
        <defs></defs>
        <g
          style="
            stroke: none;
            stroke-width: 0;
            stroke-dasharray: none;
            stroke-linecap: butt;
            stroke-linejoin: miter;
            stroke-miterlimit: 10;
            fill: none;
            fill-rule: nonzero;
            opacity: 1;
          "
          transform="translate(1.4065934065934016 1.4065934065934016) scale(2.81 2.81)"
        >
          <path
            d="M 9.478 90 c -0.768 0 -1.536 -0.293 -2.121 -0.879 c -1.172 -1.171 -1.172 -3.071 0 -4.242 L 47.236 45 L 7.357 5.121 c -1.172 -1.171 -1.172 -3.071 0 -4.242 c 1.171 -1.172 3.071 -1.172 4.242 0 l 42 42 c 0.563 0.563 0.879 1.325 0.879 2.121 s -0.316 1.559 -0.879 2.121 l -42 42 C 11.014 89.707 10.246 90 9.478 90 z"
            style="
              stroke: none;
              stroke-width: 1;
              stroke-dasharray: none;
              stroke-linecap: butt;
              stroke-linejoin: miter;
              stroke-miterlimit: 10;
              fill: rgb(0, 0, 0);
              fill-rule: nonzero;
              opacity: 1;
            "
            transform=" matrix(1 0 0 1 0 0) "
            stroke-linecap="round"
          />
          <path
            d="M 38.522 90 c -0.768 0 -1.536 -0.293 -2.121 -0.879 c -1.172 -1.171 -1.172 -3.071 0 -4.242 L 76.279 45 L 36.401 5.121 c -1.172 -1.171 -1.172 -3.071 0 -4.242 c 1.171 -1.172 3.072 -1.171 4.242 0 l 42 42 c 1.172 1.171 1.172 3.071 0 4.242 l -42 42 C 40.058 89.707 39.29 90 38.522 90 z"
            style="
              stroke: none;
              stroke-width: 1;
              stroke-dasharray: none;
              stroke-linecap: butt;
              stroke-linejoin: miter;
              stroke-miterlimit: 10;
              fill: rgb(0, 0, 0);
              fill-rule: nonzero;
              opacity: 1;
            "
            transform=" matrix(1 0 0 1 0 0) "
            stroke-linecap="round"
          />
        </g>
      </svg>
    </li>
  </ul>
</template>

<style module>
.list {
  list-style: none;
  display: flex;
}

.list li {
  border-left: 1px solid #a9a9a9;
  border-top: 1px solid #a9a9a9;
  border-bottom: 1px solid #a9a9a9;
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
  border-right: 1px solid #a9a9a9;
}

.list li:hover,
.list li:hover > svg *,
.selected_page {
  background-color: #0096ff;
  color: white;
  fill: white !important;
}
</style>
