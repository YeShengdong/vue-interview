<template>
  <div class="multi-check">
    <Card>
      <template #title>
        {{ title }}
      </template>
      <div class="card-content">
        <Checkbox :model-value="checkAll" @on-change="handleCheckAll"
          >Select All</Checkbox
        >
        <Row>
          <Col
            :span="columns"
            v-for="(ele, index) in optionsList"
            :key="index"
          >
            <CheckboxGroup
              v-model="checkGroup"
              @on-change="checkGroupChange"
            >
              <Checkbox
                v-for="item in ele"
                :key="item.value"
                :label="item.label"
                class="checkbox"
                >{{ item.label }}</Checkbox
              >
            </CheckboxGroup>
          </Col>
        </Row>
      </div>
    </Card>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export type Option = {
  label: string;
  value: string;
};

/**
 * Notice:
 * 1. There should be a special `Select All` option with checkbox to control all passing options
 * 2. If columns > 1, the options should be placed from top to bottom in each column
 *
 * @param {string} label - the label text of this component
 * @param {Option[]} options - options
 * @param {string[]} checkAllGroup - default checked option values
 * @param {number} columns - default value is 1
 * @param {Function} onChange - when checked options are changed,
 *                             they should be passed to outside
 */

export default defineComponent({
  name: "MultiCheck",
  data() {
    return {
      checkAll: false,
      checkGroup: [] as Option[],
    };
  },
  props: {
    title: {
      type: String,
      default: "多选组件",
    },
    options: {
      type: Array,
      default: [] as Option[],
    },
  },
  computed: {
    optionsList() {
      let newArr: any = [];
      for (var i = 0; i < this.options.length; i += 5) {
        newArr.push(this.options.slice(i, i + 5));
      }
      return newArr;
    },
    columns(){
      return Math.floor(24 / this.optionsList.length)
    }
  },
  methods: {
    handleCheckAll(checked: boolean) {
      this.checkAll = checked;
      if (this.checkAll) {
        this.options.forEach((item: any) => {
          this.checkGroup.push(item.label);
        });
      } else {
        this.checkGroup = [];
      }
      this.$emit("getCheckGroup", this.checkGroup);
    },
    checkGroupChange(checkGroup: string[]) {
      if (checkGroup.length == this.options.length) {
        this.checkAll = true;
      } else {
        this.checkAll = false;
      }
      this.$emit("getCheckGroup", this.checkGroup);
    },
  },
});
</script>

<style scoped lang="less">
.multi-check {
  width: 30%;
  margin: 0 auto;
  padding: 10px 0;
  .card-content {
    height: 200px;
    text-align: left;

    .checkbox {
      display: block;
      text-align: left;
    }
  }
}
/deep/ .ivu-card-head {
  background: #eee;
  text-align: left;
}
</style>
