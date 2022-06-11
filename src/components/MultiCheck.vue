<!--
 * @Author: SUN
 * @Date: 2022-06-11 10:49:22
 * @LastEditors: SUN
 * @LastEditTime: 2022-06-11 11:23:47
 * @FilePath: \vue-interview\src\components\MultiCheck.vue
-->
<template>
  <div v-for="item in options" :key="item.id">
    <label>
      <span style="font-size: 20px">{{ item.label }}:</span>
      <input
        type="checkbox"
        :checked="item.checked"
        @change="hanldeChange(item.id)"
      />
    </label>
  </div>
  <br /><br />
</template>

<script setup lang="ts">
import { defineEmits, defineProps, PropType } from "vue";

export type Option = {
  id: number;
  label: string;
  value: string;
  checked: boolean;
};
defineProps({
  options: Array as PropType<Array<Option>>,
});
const emits = defineEmits(["handleChecked"]);

const hanldeChange = (id: number) => {
  emits("handleChecked", id);
};
</script>

<style scoped lang="less">
</style>
