<script lang="ts" setup>
import {useMemory} from '@vueuse/core'

function size(v: number) {
  const kb = v / 1024 / 1024
  return `${kb.toFixed(2)} MB`
}

const {isSupported, memory} = useMemory()
</script>

<template>
  <div class="col-span-4 md:col-span-2 h-44 bg-gray-100 dark:bg-gray-800 rounded-3xl px-4 py-2">
    <div v-if="isSupported && memory" class="flex flex-col gap-4 size-full">
      <div class="text-xl font-bold leading-6">Информация о памяти браузера</div>
      <UMeterGroup :max="memory.totalJSHeapSize" size="xl">
        <template #indicator>
          <div class="text-gray-500 flex gap-1.5 justify-between text-sm">
            <p>Выделено {{ size(memory.totalJSHeapSize) }}</p>
            <p>Лимит {{ size(memory.jsHeapSizeLimit) }}</p>
          </div>
        </template>
        <UMeter
            :label="'Используется ' + size(memory.usedJSHeapSize)"
            :value="memory.usedJSHeapSize"
            color="primary"
            icon="i-heroicons-cog-6-tooth-solid"
        />
      </UMeterGroup>
    </div>
    <div v-else class="flex size-full items-center justify-center text-center text-xl font-bold">
      Ваш браузер не поддерживает API памяти производительности.
    </div>
  </div>
</template>