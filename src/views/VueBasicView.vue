<script setup lang="ts">
defineProps(['title'])

import { computed, reactive, ref, type Ref } from 'vue'

const count: Ref<number> = ref(0)

const obj = ref({
  nested: { count: 0 },
  arr: ['foo', 'bar']
})

function increment() {
  count.value++
}

function mutateDeeply() {
  // these will work as expected.
  obj.value.nested.count++
  obj.value.arr.push('baz')
}

const raw = {}
const refRaw = ref(raw)
const proxy = reactive(raw)

// proxy is NOT equal to the original.
console.log(refRaw.value === raw) // false
console.log(refRaw.value === ref(raw).value)

console.log(proxy === raw) // false
console.log(proxy === reactive(raw)) // true

const firstName = ref('John')
const lastName = ref('Doe')

const fullName = computed({
  // getter
  get() {
    return firstName.value + ' ' + lastName.value
  },
  // setter
  set(newValue) {
    // Note: we are using destructuring assignment syntax here.
    [firstName.value, lastName.value] = newValue.split(' ')
  }
})

function changeInput(e: any) {
  console.log(e);
}

fullName.value
</script>

<template>
  <div>
    <h1>Vue Basic View</h1>
    <p>{{ fullName }}</p>
    <input type="text" @change="changeInput">
  </div>
  <main>
    <button @click="increment()">{{ count }}</button>
    <div>
      <button @click="mutateDeeply()">add</button>
      <p>Data 1: {{ obj.nested.count }}</p>
      <ul>
        <li v-for="(item, index) in obj.arr" v-bind:key="index">
          {{ item }}
        </li>
      </ul>
    </div>
  </main>
</template>

<style scoped>
h1 {
  color: red;
}
</style>