<script setup lang="ts">
const modelValue = defineModel<number>('modelValue', {
  type: Number,
  required: true
})

interface Props {
  maxValue?: number
  minValue?: number
}
const props = withDefaults(defineProps<Props>(), {
  maxValue: 999,
  minValue: 1
})

function increment() {
  if (modelValue.value > props.maxValue) return
  modelValue.value += 1;
}
function decrement() {
  if (modelValue.value <= props.minValue) return
  modelValue.value -= 1;
}
</script>

<template>
  <div class="d-flex align-center">
    <VBtn
      @click="decrement"
      variant="plain"
      icon
    >
      <VIcon>mdi-minus</VIcon>
    </VBtn>

    <span class="mr-2">{{ modelValue }}</span>

    <VBtn
      @click="increment"
      variant="plain"
      icon
    >
      <VIcon>mdi-plus</VIcon>
    </VBtn>
  </div>
</template>
