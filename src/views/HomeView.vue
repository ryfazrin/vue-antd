<script setup lang="ts">
// import TheWelcome from '../components/TheWelcome.vue'
import CustomButton from '../components/CustomButton.vue'
</script>

<template>
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

  <p>outline</p>
  <CustomButton typeButton="outline">
    Hai Test
  </CustomButton>

  <p>Secondary</p>
  <CustomButton typeButton="secondary">
    Hai Test
  </CustomButton>

  <p>search</p>
  <CustomButton typeButton="search" />
</template>