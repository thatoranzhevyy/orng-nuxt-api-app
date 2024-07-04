<script setup lang="ts">
import {reactive} from 'vue'
import {useBattery} from '@vueuse/core'

const battery = reactive(useBattery())
</script>

<template>
  <div class="col-span-2 md:col-span-1 h-44 bg-gray-100 dark:bg-gray-800 rounded-3xl px-4 py-2">
    <div v-if="battery.isSupported" class="flex flex-col gap-4 size-full">
      <div v-if="battery.charging" class="text-green-500">
        <UIcon name="i-heroicons-bolt-solid" class="text-7xl" />
        <div class="text-3xl">{{ (100 * battery.level).toFixed(0) }}%</div>
      </div>
      <div v-else>
        <UIcon name="i-heroicons-battery-100-solid" class="text-7xl" />
        <div class="text-3xl">{{ (100 * battery.level).toFixed(0) }}%</div>
      </div>
    </div>
    <div v-else class="flex size-full items-center justify-center text-center text-xl font-bold">
      Данное устройство не поддерживает заряд батарей.
    </div>
  </div>
</template>