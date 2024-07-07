<script setup lang="ts">
import { usePreferredLanguages } from '@vueuse/core'
const languages = usePreferredLanguages()
</script>

<template>
  <div class="col-span-2 md:col-span-1 bg-gray-100 dark:bg-gray-800 rounded-3xl px-4 py-2">
    <div class="size-full flex flex-col items-center justify-center text-center gap-3">
      <UIcon name="i-heroicons-language-solid" class="text-7xl" />
      <div>
        <code v-for="lang in languages" :key="lang" class="mr-2">{{ lang }}</code>
      </div>
    </div>
  </div>

</template>