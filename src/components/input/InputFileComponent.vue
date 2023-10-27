<script lang="ts" setup>
import type { InputProps } from 'ant-design-vue';
import CustomButton from '../CustomButton.vue';
import { h } from 'vue';

type InputFileComponentProps = {
  preview?: string | File | any
}

const props = defineProps<InputFileComponentProps & InputProps>()
</script>

<template>
  <label 
    :for="props.disabled ? '' : `file-input-form` + (props.id ? `-${props.id}` : ``)"
    :style="{
      display: 'flex',
      flexDirection: 'column',
      cursor: props.disabled ? 'not-allowed' : 'pointer',
      ...(props.preview ? { width: 'fit-content' } : {}),
    }"
  >
    <input
      type="file"
      :id="`file-input-form` + (props.id ? `-${props.id}` : ``)"
      style="display: none;"
      @change="props.onChange"
      @blur="props.onBlur"
      :name="props.name"
      :disabled="props.disabled"
      :accept="$attrs.accept"
      :ref="$attrs.ref"
    />

    <template v-if="!props.disabled">
      <template v-if="preview">
        <span
          style="
            display: flex;
            align-items: center;
            gap: 20px;
            width: fit-content;
          "
        >
          <img
            :src="preview"
            alt="preview-image"
            width="100"
            height="100"
            style="margin-top: 20px;"
            :title="
              props.value && typeof props.value === 'string'
                ? props.value
                : ''
            "
          />
          <CustomButton
            type-button="outline"
            style="pointer-events: none;"
          >
            Browse
          </CustomButton>
        </span>
      </template>
      <template v-else>
        <span>
          <a-input
            :value="props.value"
            :placeholder="props.placeholder"
            :suffix="h(
              CustomButton,
              {
                typeButton: 'outline'
              },
              'Browse'
            )"
            :ref="$attrs.ref"
            :disabled="props.disabled"
            readonly
          />
        </span>
      </template>
    </template>
  </label>
</template>

<style lang="scss" scoped>
.ant-input {
  & :deep(.ant-input-affix-wrapper) {
    padding: 8px 16px;

    & input {
      color: #2e65f3;
    }
  }
}
</style>