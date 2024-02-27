<script setup lang="ts">
import { ref, computed } from 'vue';
import highlight from 'highlight.js'
import { useDark, useClipboard, useStorage } from '@vueuse/core'
import { ColorPick, ThemeSwitch, HighlightCode, Counter } from '@/components'
//
const className = useStorage('className', 'body')
const thumbColor = useStorage('thumbColor', '#6baf8d')
const trackColor = useStorage('trackColor', '#455054')
const thumbBorderColor = useStorage('thumbBorderColor', '#c71111')

const scrollbarWidth = useStorage('scrollbarWidth', 20)
const scrollBarborderRadius = useStorage('scrollBarborderRadius', 0)
const thumbBorderWidth = useStorage('thumbBorderWidth', 6)

const thumbColorPick = ref(false)
const trackColorPick = ref(false)
const thumbBorderColorPick = ref(false)
</script>


<template>
  <VApp>
    <VMain>
      <div class="d-flex align-center text-h3 justify-center my-4">
        <VIcon
          color="teal"
          start
        >
          mdi-rollerblade
        </VIcon>
        <span>
          Scrollbar
        </span>
      </div>
      <VContainer>
        <VContainer>
          <VRow justify="space-evenly">
            <VCol
              cols="12"
              lg="4"
              md="4"
              sm="4"
            >
              <h4 class="text-h4 mb-4">Settings</h4>
              <div class="d-flex justify-space-between align-center my-4">
                <span>Theme</span>
                <ThemeSwitch />
              </div>
              <div class="d-flex justify-space-between align-center my-4">
                <span>Class Name</span>
                <VTextField
                  v-model="className"
                  hide-details
                  hide-spin-buttons
                  variant="outlined"
                  density="compact"
                  class="ml-4"
                />
              </div>
              <div class="d-flex justify-space-between align-center my-4">
                <span>Thumb Color</span>
                <ColorPick
                  v-model:model-value="thumbColorPick"
                  v-model:color="thumbColor"
                />
              </div>
              <div class="d-flex justify-space-between align-center my-4">
                <span>Track Color</span>
                <ColorPick
                  v-model:model-value="trackColorPick"
                  v-model:color="trackColor"
                />
              </div>
              <div class="d-flex justify-space-between align-center my-4">
                <span>Scrollbar Width: </span>
                <Counter v-model="scrollbarWidth" />
              </div>
              <div class="d-flex justify-space-between align-center my-4">
                <span>Scrollbar Border Radius: </span>
                <Counter
                  v-model="scrollBarborderRadius"
                  :min-value="0"
                />
              </div>
              <div class="d-flex justify-space-between align-center my-4">
                <span>Thumb Border Width</span>
                <Counter v-model="thumbBorderWidth" />
              </div>
              <div class="d-flex justify-space-between align-center my-4">
                <span>Thumb Border Color</span>
                <ColorPick
                  v-model:model-value="thumbBorderColorPick"
                  v-model:color="thumbBorderColor"
                />
              </div>
            </VCol>
            <VCol
              cols="12"
              lg="7"
              md="7"
              sm="7"
            >
              <h4 class="text-h4  mb-4">Code</h4>
              <HighlightCode
                :class-name="className"
                :thumb-color="thumbColor"
                :track-color="trackColor"
                :thumb-border-color="thumbBorderColor"
                :scrollbar-width="scrollbarWidth"
                :scroll-barborder-radius="scrollBarborderRadius"
                :thumb-border-width="thumbBorderWidth"
              />
            </VCol>
          </VRow>
        </VContainer>
      </VContainer>
    </VMain>
  </VApp>
</template>
