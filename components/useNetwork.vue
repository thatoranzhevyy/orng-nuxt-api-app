<script setup lang="ts">
import {reactive} from 'vue'
import {useNetwork} from '@vueuse/core'

const network = reactive(useNetwork())
</script>

<template>
  <div class="col-span-2 md:col-span-1 h-44 bg-gray-100 dark:bg-gray-800 rounded-3xl px-4 py-2">
    <div v-if="network.isSupported" class="flex flex-col gap-4 size-full">
      <div v-if="network.isOnline" class="text-green-500">
        <UIcon name="i-heroicons-globe-alt-solid" class="text-7xl"/>
      </div>
      <div v-else class="text-red-500">
        <UIcon name="i-heroicons-globe-alt-solid" class="text-7xl"/>
      </div>
    </div>
    <div v-else class="flex size-full items-center justify-center text-center text-xl font-bold">
      Данное устройство не поддерживает заряд батарей.
    </div>
  </div>
</template>