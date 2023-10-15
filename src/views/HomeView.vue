<script setup lang="ts">
// import TheWelcome from '../components/TheWelcome.vue'
import CustomButton from '../components/CustomButton.vue'
import { Button } from 'ant-design-vue'
</script>

<template>
  <!-- <Button>Test</Button> -->
  <p>Add</p>
  <CustomButton typeButton="add">
    Hai Test
  </CustomButton>

  <p>Filter</p>
  <CustomButton typeButton="filter">
    Hai Test
  </CustomButton>
</template>