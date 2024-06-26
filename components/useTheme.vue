<script setup lang="ts">
const colorMode = useColorMode();
const isDark = computed({
  get() {
    return colorMode.value === "dark";
  },
  set() {
    colorMode.preference = colorMode.value === "dark" ? "light" : "dark";
  }
});
</script>

<template>
  <div class="col-span-2 md:col-span-1 h-44 bg-gray-100 dark:bg-gray-800 rounded-3xl px-4 py-2" @click="isDark = !isDark">
    <div class="size-full flex flex-col items-center justify-center text-center gap-2">
      <div v-if="isDark">
        <UIcon name="i-heroicons-moon-solid" class="text-7xl" />
      </div>
      <div v-else>
        <UIcon name="i-heroicons-sun-solid" class="text-7xl" />
      </div>
      {{colorMode.value}}
    </div>
  </div>
</template>
