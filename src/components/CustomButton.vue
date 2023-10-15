<script setup lang="ts">
import { Button, type ButtonProps } from 'ant-design-vue'
import { COLORS, type ColorType } from '@/styles/color.ts'

type CustomButtonProps = {
  typeButton?:
  | 'primary'
  | 'secondary'
  | 'danger'
  | 'add'
  | 'download'
  | 'filter'
  | 'search'
  | 'outline';
  isStrong?: boolean;
  outlineType?: ColorType;
  isInverted?: boolean;
};

const props = withDefaults(
  defineProps<CustomButtonProps & ButtonProps>(),
	// Props Default value
  {
    typeButton: 'primary',
    isStrong: true,
    isInverted: false,
  }
);

const theme = {
	customClass: props.typeButton === 'secondary' 
		? 'secondary-button'
		: ['filter', 'search', 'outline'].includes(props.typeButton)
		? 'outline-button' : '',
	icon: ['add', 'download', 'filter', 'search'].includes(props.typeButton) ?
		props.typeButton === 'add'
			? 'Plus Icon'
			: props.typeButton === 'filter'
			? 'filter Icon'
			: props.typeButton === 'search'
			? 'Search Icon'
			: 'Download Icon' : null,
  $outlineColor: props.outlineType ? COLORS[props.outlineType] : '',
}
</script>

<!-- <style scoped lang="scss">
.ant-btn {
  background: v-bind('props.typeButton === `danger` ? `#DC3545` : `radial-gradient(76.32% 76.32% at 95.23% 6.02%, #9358AF 0%, #7E5AC6 54.71%, rgba(142, 80, 220, 0.00) 100%), linear-gradient(72deg, #9A57A7 0%, rgba(106, 103, 227, 0.00) 100%), radial-gradient(45.63% 45.63% at 35.11% -11.02%, #7936AE 0%, rgba(95, 34, 143, 0.00) 100%), radial-gradient(156.61% 80.36% at 94.32% 94.43%, rgba(123, 83, 184, 0.78) 0%, rgba(124, 92, 199, 0.78) 32.29%, rgba(145, 105, 208, 0.37) 64.06%, rgba(105, 43, 205, 0.00) 100%), linear-gradient(313deg, #9557AD 0%, #604AEA 100%)`');
  font-weight: v-bind('props.isStrong ? `700` : `400`');
  position: relative;
  box-shadow: none;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 10px 20px;
  line-height: 16px !important;

  &:hover {
    /* background: v-bind('theme.$typeButton'); */
  }

  &.secondary-button {
		&::before {
			content: '';
			position: absolute;
			top: 0.5px;
			left: 0.5px;
			width: calc(100% - 1px);
			height: calc(100% - 0.5px);
			border-radius: 9px;
			background-color: #fff;
			z-index: 1;
		}

		& span {
			z-index: 2;
			position: relative;
			line-height: 1;

			/* Gradient/Avrist Light */
			background: radial-gradient(
						62.61% 62.61% at 95.23% 6.02%,
						#9358af 0%,
						#7e5ac6 54.71%,
						rgba(142, 80, 220, 0) 100%
					)
					/* warning: gradient uses a rotation that is not supported by CSS and may not behave as expected */,
				linear-gradient(72.48deg, #9a57a7 2.61%, rgba(106, 103, 227, 0) 56.18%),
				radial-gradient(
						45.23% 45.23% at 35.11% -11.02%,
						#7936ae 0%,
						rgba(95, 34, 143, 0) 100%
					)
					/* warning: gradient uses a rotation that is not supported by CSS and may not behave as expected */,
				radial-gradient(
						94.51% 124.88% at 94.32% 94.43%,
						rgba(123, 83, 184, 0.78) 0%,
						rgba(124, 92, 199, 0.78) 32.29%,
						rgba(145, 105, 208, 0.3666) 64.06%,
						rgba(105, 43, 205, 0) 100%
					)
					/* warning: gradient uses a rotation that is not supported by CSS and may not behave as expected */,
				linear-gradient(313.04deg, #9557ad 0.93%, #604aea 125.68%);
			-webkit-background-clip: text;
			-webkit-text-fill-color: transparent;
			background-clip: text;
		}
	}

	&.outline-button {
		background: v-bind('props.outlineType ? props.isInverted ? `#fff` : props.outlineType : `#fff`');
	}
}
</style> -->

<template>
  <Button
		v-bind="props"
		:icon="theme.icon"
		:class="[$attrs.class, theme.customClass]">
		<!-- {{ $attrs.class }} | {{ theme.customClass }} -->
    <slot />
  </Button>
</template>