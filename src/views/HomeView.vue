<template>
  <h1>Multi Check Component</h1>
  <MultiCheck :title="'Status'" :options='options' @getCheckGroup='getCheckGroup'/>
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
        { label: "Under", value: "666" },
        { label: "ggg", value: "777" },
        { label: "hhh", value: "888" },
        { label: "iii", value: "999" },
        { label: "kkk", value: "929" },
        { label: "lll", value: "939" },
        { label: "mmm", value: "949" },
      ] as Option[],
      selectedValues: [] as string[],
    };
  },
  methods:{
    getCheckGroup(data: string[]){
      this.selectedValues= data
    }
  }
});
</script>
