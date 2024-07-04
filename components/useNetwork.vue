<script setup lang="ts">
import { useOnline } from '@vueuse/core'

const online = useOnline()
</script>

<template>
  <div class="col-span-2 md:col-span-1 h-44 bg-gray-100 dark:bg-gray-800 rounded-3xl px-4 py-2">
    <div class="flex flex-col gap-4 size-full items-center justify-center">
      <div v-if="online" class="text-green-500">
        <UIcon name="i-heroicons-globe-alt-solid" class="text-7xl"/>
      </div>
      <div v-else class="text-red-500">
        <UIcon name="i-heroicons-globe-alt-solid" class="text-7xl"/>
      </div>
    </div>
  </div>
</template>