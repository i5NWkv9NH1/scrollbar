<script setup lang="ts">
const modelValue = defineModel<boolean>('modelValue', {
  type: Boolean,
  required: true
})
const color = defineModel<string>('color', {
  type: String,
  required: true
})
interface Props {
  size?: number
  offset?: number
}
const props = withDefaults(defineProps<Props>(), {
  size: 24,
  offset: 10
})
</script>

<template>
  <VMenu
    v-model="modelValue"
    :close-on-content-click="false"
    :offset="props.offset"
    transition="slide-y-transition"
  >
    <template #activator="activator">
      <VAvatar
        :size="props.size"
        v-bind="activator.props"
        :color="color"
        rounded="lg"
      />
    </template>
    <template #default>
      <VCard>
        <VColorPicker
          v-model="color"
          mode="hex"
        />
      </VCard>
    </template>
  </VMenu>
</template>
