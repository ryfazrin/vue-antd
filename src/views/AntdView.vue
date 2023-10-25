<script lang="ts" setup>
import type { SelectProps } from 'ant-design-vue';
import { ref } from 'vue';
import SelectComponent from '../components/SelectComponent.vue'
import type { SelectValue } from 'ant-design-vue/es/select';

const value1 = ref('lucy')
const options1 = ref<SelectProps['options']>([
  {
    value: 'jack',
    label: 'Jack',
  },
  {
    value: 'lucy',
    label: 'Lucy',
  },
  {
    value: 'disabled',
    label: 'Disabled',
    disabled: true,
  },
  {
    value: 'yiminghe',
    label: 'Yiminghe',
  },
])
const focus = () => {
  console.log('focus');
}

const handleChange = (value: SelectValue) => {
  console.log(`selected ${value}`);
}
</script>

<template>
  <div style="padding: 10px;">
    <SelectComponent
      ref="select"
      v-model:value="value1"
      :options="options1"
      @change="handleChange"
      @focus="focus"
      style="width: 120px"
    ></SelectComponent>
  </div>
</template>

<style scoped>

</style>
