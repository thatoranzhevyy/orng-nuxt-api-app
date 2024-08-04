<script lang="ts">
import {ref, onMounted} from 'vue';

export default {
  setup() {
    const recentTracks = ref([]);

    const fetchData = async () => {
      const username = "oranzhevyy"
      const key = 'df9ebdae99abc2fabf3c55ceb195e1db'
      try {
        const response = await fetch(
            `https://ws.audioscrobbler.com/2.0/?method=user.getrecenttracks&user=${username}&api_key=${key}&limit=1&format=json`
        )
        const data = await response.json()
        recentTracks.value = data.recenttracks.track; // Assuming the response contains an array of data
      } catch (error) {
        // Handle any errors
      }
      // const timer = setInterval(fetchData, 60000);
    };

    onMounted(() => {
      fetchData();
    });

    return {
      recentTracks,
    };
  },
};

</script>

<template>
  <div class="col-span-4 md:col-span-2 bg-gray-100 dark:bg-gray-800 rounded-xl px-4 py-2">
    <div v-if="recentTracks.length>0" class="flex gap-6 size-full items-center">
      <img class="size-32 rounded-md bg-gray-100 dark:bg-gray-900" :src="recentTracks[0].image[2]['#text']"/>
      <div>
        <div>{{ recentTracks[0].artist['#text'] }}</div>
        <div>{{ recentTracks[0].name }}</div>
      </div>
    </div>
    <div v-else class="flex gap-6 size-full items-center">
      <USkeleton class="size-32 bg-gray-100 dark:bg-gray-900"/>
      <div class="space-y-2">
        <USkeleton class="h-4 w-[200px] bg-gray-100 dark:bg-gray-900"/>
        <USkeleton class="h-4 w-[160px] bg-gray-100 dark:bg-gray-900"/>
      </div>
    </div>
  </div>
</template>