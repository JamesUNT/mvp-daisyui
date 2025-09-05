<template>
  <main>
    <div class="p-4">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <card-base
          v-for="episodio in episodios"
          :key="episodio.id"
          :titulo="episodio.name"
          :episodio="episodio.episode"
          :lancamento="episodio.air_date"
          :personagens="episodio.characters"
        />
      </div>
    </div>
  </main>
</template>

<script setup>
import axios from 'axios'

const episodios = ref([])

async function handleGetEpisodes() {
  try {
    const response = await axios.get('https://rickandmortyapi.com/api/episode')
    episodios.value = response.data.results
  } catch (error) {
    console.error('Error fetching episodes:', error)
  }
}

onMounted(async () => {
  await handleGetEpisodes()
})
</script>
