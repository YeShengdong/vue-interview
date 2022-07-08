<template>
    <div>@todo</div>
    <p style="margin: auto;text-align: center; border: 1px solid #000; border-bottom: none;" :style="{width: containerWidth}">
      {{label}}
    </p>
    <div :style="{width: containerWidth, margin: 'auto'}" class="container">
      <div :key="columnIndex" v-for="(columnItem, columnIndex) in checkboxData" :style="{height: columnHeight}">
        <p v-if="columnIndex === 0">
          <input type="checkbox" :checked="checkedAll" @click="selectAll"> selectAll
        </p>
         <p :key="item.value" v-for="item in columnItem">
        
           <input  type="checkbox" :value="item.value"   v-model="selectValues"> {{item.label}}
        </p>
      </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

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
 * @param {string[]} values - default checked option values
 * @param {number} columns - default value is 1
 * @param {Function} onChange - when checked options are changed,
 *                             they should be passed to outside
 */

export default defineComponent({
  name: 'MultiCheck',
  props: {
    label: {
      type: String,
      default: 'select'
    },
    options: {
      type: Array,
      default: () => {
        return []
      }
    },
    values: {
      type: Array,
      default: () => {
        return []
      }
    },
    number: {
      type: Number,
      default: 2
    }
  },
  data () {
    return {
       checkboxData: [] as any[],
       //values: []
       checkedAll: false,
       selectValues: [] as any[],
       columnHeight: ''
    } 
  },
  created() {
    this.initData()
  },
  watch: {
    selectValues(newVal) {
      if(newVal.length === this.options.length) {
         this.checkedAll = true
      }else {
        this.checkedAll = false
      }
      this.$emit('onChange', newVal)
    }
  },
  methods: {
    initData() {
       this.selectValues = this.values
       let colCount = Math.ceil(this.options.length / this.number)
       this.columnHeight =  (colCount + 1) * 22 + 'px'
       if(colCount >= this.options.length) {
         this.checkboxData.push([...this.options])
       }else {
         let cur = 0
         while(cur < this.options.length) {
           if(cur + colCount < this.options.length) {
             this.checkboxData.push([...this.options.slice(cur, cur + colCount)])
           }else {
             this.checkboxData.push([...this.options.slice(cur, this.options.length)])
           }
            cur = cur + colCount
         }
       }
       while(this.checkboxData.length < this.number) {
         this.checkboxData.push([])
       }
    },
    selectAll (e: Event) {
    let checked = (e.target as HTMLInputElement).checked
    if(checked){
        this.selectValues = this.options.map( (item:any) => {
          
          return item.value
      }) 
        
     }else {
       this.selectValues = []
     }
     this.$emit('onChange', this.selectValues)

  
    }
  },
  computed: {
    containerWidth () {
      return this.number * 300 + 'px'
    }
  }

});
</script>

<style scoped lang="less">
p {
  margin: 0;
}
.container{
  &::after{
    content: '';
    clear: both;
    display: block;
  }
  div {
    width: 300px;
    float: left;
    box-sizing: border-box;
    border: 1px solid #000;
    p{
      
      text-align: left;
      text-overflow: ellipsis;
      overflow:hidden;
      white-space: nowrap;
    }
  }
  div:nth-child(n + 2){
    border-left: none;
  }
}
</style>
