<script setup lang="ts">
import { computed, ref } from 'vue';
import highlight from 'highlight.js/lib/core'
import css from 'highlight.js/lib/languages/css';
import { useClipboard } from '@vueuse/core'


highlight.registerLanguage('css', css)

interface Props {
  className: string
  thumbColor: string
  trackColor: string
  thumbBorderColor: string
  scrollbarWidth: number
  scrollBarborderRadius: number
  thumbBorderWidth: number
}
const props = defineProps<Props>()




const code = computed(() => (`
    ${props.className} {
      --sb-thumb-color: ${props.thumbColor};
      --sb-track-color: ${props.trackColor};
      --sb-size: ${props.scrollbarWidth}px;
    }

    ${props.className}::-webkit-scrollbar {
      width: var(--sb-size)
    }

    ${props.className}::-webkit-scrollbar-track {
      background: var(--sb-track-color);
      border-radius: ${props.scrollBarborderRadius}px;
    }

    ${props.className}::-webkit-scrollbar-thumb {
      background: var(--sb-thumb-color);
      border-radius: ${props.scrollBarborderRadius};
      border: ${props.thumbBorderWidth}px solid ${props.thumbBorderColor};
    }

    @supports not selector(::-webkit-scrollbar) {
      ${props.className} {
        scrollbar-color: var(--sb-thumb-color)
                        var(--sb-track-color);
      }
    }
`))
const highlightCode = computed(() => {
  return highlight.highlight(code.value, { language: 'css' }).value
})
const { text, copy, isSupported, copied } = useClipboard({ source: code, })

</script>

<style lang="scss">
@use "sass:meta";

html[data-theme="light"] {
  @include meta.load-css("highlight.js/scss/github.scss");
}

html[data-theme="dark"] {
  @include meta.load-css("highlight.js/scss/stackoverflow-dark.scss");
}

code {
  --thumb-color: v-bind(thumbColor);
  --track-color: v-bind(trackColor);
  ---thumb-border-color: v-bind(thumbBorderColor);
  --size: v-bind(scrollbarWidth + "px");
  --radisu-size: v-bind(scrollBarborderRadius + "px");
  --border-size: v-bind(thumbBorderWidth + "px");

  height: 500px;
}

code::-webkit-scrollbar {
  width: var(--size);
}

code::-webkit-scrollbar-track {
  background: var(--track-color);
  border-radius: var(--border-size);
}

code::-webkit-scrollbar-thumb {
  background: var(--thumb-color);
  border-radius: var(--radisu-size);
  border: var(--border-size) solid var(---thumb-border-color);
}

@supports not selector(::-webkit-scrollbar) {
  code {
    scrollbar-color: var(--thumb-color) var(--track-color);
  }
}
</style>

<template>
  <VSheet
    elevation="4"
    class="my-4"
  >
    <pre>
      <code class="hljs hljs-css" v-html="highlightCode" />
    </pre>
  </VSheet>
  <VBtn
    v-if="isSupported"
    size="x-large"
    elevation="4"
    color="primary"
    @click="copy(code)"
  >
    {{ copied ? 'Copied!' : 'Copy' }}
  </VBtn>
</template>
