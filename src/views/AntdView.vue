<script lang="ts" setup>
import type { SelectProps } from 'ant-design-vue';
import { watch, ref } from 'vue';
import SelectComponent from '../components/SelectComponent.vue'
import ButtonAction from '../components/ButtonAction.vue'
import ModalConfirmationDelete from '../components/ModalConfirmationDelete.vue'
import InputComponent from '../components/input/InputComponent.vue'
import CustomContainerActionChange from '../components/organisms/CustomContainerActionChange.vue'
import InputPasswordComponent from '../components/input/InputPasswordComponent.vue'
import InputFileComponent from '../components/input/InputFileComponent.vue'
import TextAreaComponent from '../components/input/TextAreaComponent.vue'
import type { SelectValue } from 'ant-design-vue/es/select';
import CustomButton from '@/components/CustomButton.vue';
import FilterStatusMain from '@/components/FilterStatusMain.vue';
import ButtonInputComponent from '@/components/ButtonInputComponent.vue';
import CustomTable from '@/components/CustomTable.vue';

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

// Modal Delete
const openModalDelete = ref<boolean>(false)

const showModalDelete = () => {
  openModalDelete.value = true
}
const onConfirmationDelete = (isConfirm: boolean) => {
  console.log(isConfirm)
  openModalDelete.value = false
}

// FilterStatusMain
const onChangeStatus = (e: any) => {
  console.log(e);
}

// Table
const columns = [
  {
    name: 'Name',
    dataIndex: 'name',
    key: 'name',
  },
  {
    title: 'Age',
    dataIndex: 'age',
    key: 'age',
  },
  {
    title: 'Address',
    dataIndex: 'address',
    key: 'address',
  },
  {
    title: 'Tags',
    key: 'tags',
    dataIndex: 'tags',
  },
  {
    title: 'Action',
    key: 'action',
  },
];

const data = [
  {
    key: '1',
    name: 'John Brown',
    age: 32,
    address: 'New York No. 1 Lake Park',
    tags: ['nice', 'developer'],
  },
  {
    key: '2',
    name: 'Jim Green',
    age: 42,
    address: 'London No. 1 Lake Park',
    tags: ['loser'],
  },
  {
    key: '3',
    name: 'Joe Black',
    age: 32,
    address: 'Sidney No. 1 Lake Park',
    tags: ['cool', 'teacher'],
  },
];

// CustomContainerActionChange
const onSubmit = () => console.log('submit')
const onReset = () => console.log('reset')
</script>

<template>
  <div style="padding: 10px;">
    <!-- :addLoading="isLoadingCreate || isLoadingEdit" -->
    <CustomContainerActionChange
      text="Kamu bisa menambahkan data disini dengan mengklik save."
      addText="Save"
      :addIcon="false"
      :addLoading="false"
      resetText="Cancel"
      @add="onSubmit"
      @reset="onReset"
    />
    <p>Custom Table</p>
    <CustomTable
      :columns="columns"
      :data-source="data"
    />
    <p>Button Input Component</p>
    <ButtonInputComponent 
      placeholder="Search..."
      @search="(e) => console.log(e)"
    />
    <p>Button Action</p>
    <ButtonAction
      type-action="remove"
      @delete="() => console.log('delete lagi')" />
    
    <ButtonAction
      type-action="refresh"
      @refresh="() => console.log('refresh lagi')" />

    <FilterStatusMain @change-status="onChangeStatus" />

    <p>Modal Confirmation delete</p>
    <!-- <CustomButton type="primary" @click="showModalDelete">Open Modal Delete</CustomButton>
    <ModalConfirmationDelete
      v-model:is-open="openModalDelete"
      @close="onConfirmationDelete"
      title="Delete" /> -->

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
