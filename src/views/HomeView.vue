<template>
  <h1>Multi Check Component</h1>
  <MultiCheck :options="options" @handleChecked="handleChecked" />
  <div>
    <label>
      <span>Select All: </span>
      <input type="checkbox" @change="handleCheckAll" :checked="checkedAll" />
    </label>
    <h2>Current selected values:</h2>
    <div>{{ selectedValues.join(",") }}</div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref, computed } from "vue";
import MultiCheck, { Option } from "@/components/MultiCheck.vue";

const options = reactive<Option[]>([
  { id: 1, label: "aaa", value: "111", checked: false },
  { id: 2, label: "bbb", value: "222", checked: false },
  { id: 3, label: "ccc", value: "333", checked: true },
  { id: 4, label: "ddd", value: "444", checked: true },
  { id: 5, label: "eee", value: "555", checked: false },
  { id: 6, label: "Under Agreement", value: "666", checked: false },
  { id: 7, label: "ggg", value: "777", checked: false },
  { id: 8, label: "hhh", value: "888", checked: false },
  { id: 9, label: "iii", value: "999", checked: false },
]);

let checkedOptions = reactive<Option[]>([]);

const checkedAll = ref<boolean>(false);

const handleChecked = (id: number) => {
  checkedOptions = [];
  for (let item of options) {
    if (id === item.id) item.checked = !item.checked;
    if (item.checked) checkedOptions.push(item);
  }
  checkedAll.value = checkedOptions.length === options.length ? true : false;
};

const handleCheckAll = () => {
  checkedAll.value = !checkedAll.value;
  for (const item of options) {
    item.checked = checkedAll.value;
  }
};

const selectedValues = computed(() => {
  const tempArr = [];
  for (const item of options) {
    if (item.checked) tempArr.push(item.label);
  }
  return tempArr;
});
</script>
