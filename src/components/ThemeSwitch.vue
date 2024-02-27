<script setup lang="ts">
import { computed, watch } from 'vue';
import { useDark, useToggle } from '@vueuse/core'
import { useTheme } from 'vuetify/lib/framework.mjs';

const vuetify = useTheme()
const isDark = useDark({
  storageKey: 'theme',
  attribute: 'data-theme',
  valueDark: 'dark',
  valueLight: 'light'
})
const toggle = useToggle(isDark)
const theme = computed(() => isDark.value ? 'dark' : 'light')
watch(theme, () => {
  vuetify.global.name.value = theme.value
}, { immediate: true })
</script>

<template>
  <VBtn @click="toggle()">
    <VIcon start>
      {{ theme === 'dark' ? 'mdi-weather-night' : 'mdi-white-balance-sunny' }}
    </VIcon>
    <span>{{ theme }}</span>
  </VBtn>
</template>
