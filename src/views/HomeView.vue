<template>
  <h1>Multi Check Component</h1>
  <MultiCheck />
  <div>
    <h2>Current selected values:</h2>
    <div>{{ selectedValues.join(",") }}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import MultiCheck, { Option } from "@/components/MultiCheck.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    MultiCheck,
  },
  data() {
    return {
      options: [
        { label: "aaa", value: "111" },
        { label: "bbb", value: "222" },
        { label: "ccc", value: "333" },
        { label: "ddd", value: "444" },
        { label: "eee", value: "555" },
        { label: "Under Agreement", value: "666" },
        { label: "ggg", value: "777" },
        { label: "hhh", value: "888" },
        { label: "iii", value: "999" },
      ] as Option[],
      selectedValues: [] as string[],
    };
  },
});
</script>
