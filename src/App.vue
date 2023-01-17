<script setup>
import { ref } from 'vue'
import SearchForm from '@/components/SearchForm.vue'
import Result from '@/components/Result.vue'

const query = ref('powfu')
const trackList = ref(null)

const searchTrack = async () => {
  const res = await fetch('https://api.deezer.com/search?q='+query.value)
    .then(r => r.json())
  trackList.value = res["data"]
}

</script>

<template>
  <SearchForm v-model="query" @search="searchTrack" />
  <Result :trackList="trackList" />
</template>
