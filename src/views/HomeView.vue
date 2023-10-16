<script setup lang="ts">
// import TheWelcome from '../components/TheWelcome.vue'
import TestDua from '../components/TestDua.vue';
import CustomButton from '../components/CustomButton.vue'
import { Button } from 'ant-design-vue'
</script>

<template>
  <!-- <Button>Test</Button> -->
  <TestDua />
  <p>Add</p>
  <CustomButton typeButton="add">
    Hai Test
  </CustomButton>

  <p>Filter</p>
  <CustomButton typeButton="filter">
    Hai Test
  </CustomButton>

  <p>Danger</p>
  <CustomButton typeButton="danger">
    Hai Test
  </CustomButton>

  <p>Secondary</p>
  <CustomButton typeButton="secondary">
    Hai Test
  </CustomButton>

  <p>search</p>
  <CustomButton typeButton="search" />
</template>