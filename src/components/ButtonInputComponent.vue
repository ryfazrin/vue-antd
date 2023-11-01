<script lang="ts" setup>
import { SearchOutlined } from '@ant-design/icons-vue';
import CustomButton from './CustomButton.vue';
import InputComponent from './InputComponent.vue';
import { h, ref, watch } from 'vue';
import { debounce } from '../utils/debounce';

interface ButtonInputComponentProps {
  onSearch: (e: any) => void
	placeholder: string
}

const props = defineProps<ButtonInputComponentProps>()

// TODO router

const isFocusInput = ref(false)
const inputValue = ref('')

const inputRef = ref<any>()

const onFocusInput = () => {
  // console.log('clicked')
  isFocusInput.value = true
}

const onBlurInput = (e: any) => {
  const value_input = e?.target?.value;

  if (!value_input) {
    isFocusInput.value = false
  }
}

const onChangeInput = debounce((e: any) => {
  if (e?.target?.value?.length >= 3 || !e?.target?.value?.length) {
    console.log(e?.target?.value)
    props.onSearch(e);
  }
  /* else {
    onSearch(undefined);
  } */
})

// TODO effects
watch(isFocusInput, (newValue) => {
  if (newValue && inputRef.value?.current) {
    inputRef.value.current.focus();
  }
})
</script>

<template>
  <template v-if="!isFocusInput">
    <CustomButton 
      type-button="search"
      @click="onFocusInput"
    />
  </template>

  <!-- TODO onBlur, onChange, onKeyDown -->
  <template v-if="isFocusInput">
    <InputComponent
      id="search-list-component"
      :placeholder="placeholder"
      :title="placeholder"
      :prefix="h(SearchOutlined)"
      :ref="inputRef"
      :default-value="inputValue"
      @blur="onBlurInput"
      @change="onChangeInput"
      @keydown.enter="(e) => props.onSearch(e)"
      style="
        background: #fff;
        height: 44px;
        padding: 10px 10px 10px 16px;
        font-size: 16px;
        line-height: 24px;
      "
    />
  </template>
</template>

<style lang="scss" scoped></style>