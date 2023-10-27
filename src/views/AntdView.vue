<script lang="ts" setup>
import type { SelectProps } from 'ant-design-vue';
import { watch, ref } from 'vue';
import SelectComponent from '../components/SelectComponent.vue'
import ModalComponent from '../components/ModalComponent.vue'
import InputComponent from '../components/input/InputComponent.vue'
import InputPasswordComponent from '../components/input/InputPasswordComponent.vue'
import InputFileComponent from '../components/input/InputFileComponent.vue'
import TextAreaComponent from '../components/input/TextAreaComponent.vue'
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

const value = ref<string>('')
watch(value, () => {
  console.log(value.value)
})

// Modal
const openModal = ref<boolean>(false)

const showModal = () => {
  openModal.value = true
};

const handleOkModal = (e: MouseEvent) => {
  console.log(e)
  openModal.value = false
}
</script>

<template>
  <div style="padding: 10px;">
    <a-button type="primary" @click="showModal">Open Modal</a-button>
    <ModalComponent v-model:open="openModal" title="Basic Modal" @ok="handleOkModal">
      <p>Some contents...</p>
      <p>Some contents...</p>
      <p>Some contents...</p>
    </ModalComponent>

    <SelectComponent
      ref="select"
      v-model:value="value1"
      :options="options1"
      @change="handleChange"
      @focus="focus"
      style="
        width: 120px;
        height: 44px;
      "
    ></SelectComponent>

    <InputFileComponent ref="inputFile1" :disabled="false" :preview="true" />
    <InputFileComponent ref="inputFile2" :disabled="false" :preview="false" />
    <InputComponent v-model:value="value" placeholder="Basic usage" />
    <InputPasswordComponent v-model:value="value" placeholder="Basic usage" />
    <TextAreaComponent v-model:value="value" placeholder="Basic usage" />
  </div>
</template>

<style scoped>

</style>
