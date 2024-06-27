<script lang="ts" setup>
const username = "oranzhevyy"
const key = 'df9ebdae99abc2fabf3c55ceb195e1db'
const response = await fetch(
    `https://ws.audioscrobbler.com/2.0/?method=user.getrecenttracks&user=${username}&api_key=${key}&limit=1&format=json`
)
const data = await response.json()
let recentTracks = data.recenttracks.track
</script>

<template>
  <div class="col-span-4 md:col-span-2 h-44 bg-gray-100 dark:bg-gray-800 rounded-3xl px-4 py-2">
    <div class="flex gap-6 size-full items-center">
      <img class="size-32 bg-gray-100 dark:bg-gray-900" :src="recentTracks[0].image[2]['#text']"/>
      <div>
        <div>{{ recentTracks[0].artist['#text'] }}</div>
        <div>{{ recentTracks[0].name }}</div>
      </div>
    </div>
  </div>
</template>