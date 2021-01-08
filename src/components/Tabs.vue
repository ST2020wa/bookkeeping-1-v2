<template>
    <ul class="tabs" :class="{[classPrefix+'-tabs']: classPrefix}">
      <li v-for="item in dataSource" :key="item.value" class="tabs-item"
          :class="liClass(item)" @click="select(item)">{{item.text}}
      </li>
    </ul>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component, Prop} from 'vue-property-decorator';
type DataSourceItem = { text: string; value: string }

@Component
export default class Tabs extends Vue {
  @Prop({required: true, type: Array})
  dataSource!: DataSourceItem[];
  @Prop(String)
  readonly value!: string;
  @Prop(String)
  classPrefix?: string;
  @Prop({type: String, default: '64px'})
  height!: string;

  liClass(item: DataSourceItem) {
    return {
      [this.classPrefix + '-tabs-item']: this.classPrefix,
      selected: item.value === this.value
    };
  }

  select(item: DataSourceItem) {
    this.$emit('update:value', item.value);
  }
}
</script>

<style lang="scss" scoped>
$bg: #f2f2f2;
 .tabs {
   width: 100%;
   display: flex;
   text-align: center;
   margin: 0 auto;
   font-size: 20px;

   &-item {
     width: 50%;
    height: 48px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
     border-radius: 48px;

    &.selected::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 48px;
      border-radius: 48px;
      background: rgb(124,84,255,0.25);
    }
  }
}
</style>