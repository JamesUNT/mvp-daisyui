<template>
  <main>
    <div class="p-4">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <card-base
          v-for="episodio in episodios"
          :key="episodio.id"
          :id="episodio.id"
          :titulo="episodio.name"
          :episodio="episodio.episode"
          :lancamento="episodio.air_date"
          :personagens="episodio.characters"
          @card-click="cardClick"
        />
      </div>
    </div>
    <div class="flex justify-center py-4">
      <div class="join" v-for="(pagina, index) in totalPaginas" :key="index">
        <button
          class="join-item btn btn-lg md:btn-md lg:btn-sm"
          :class="{ 'btn-active': paginaAtual === index + 1 }"
          @click="setPagination(index + 1)"
        >
          {{ index + 1 }}
        </button>
      </div>
    </div>
    <modal-episode
      v-if="episodioIndividual"
      :episodio="episodioIndividual"
      :personagens="personagens"
      :id="episodioId"
    />
  </main>
</template>

<script setup>
import axios from 'axios'

const episodios = ref([])
const episodioId = ref('')
const paginaAtual = ref(1)
const totalPaginas = ref(0)
//---------------------------------
const episodioIndividual = ref(null)
const personagens = ref([])

async function cardClick(id) {
  episodioId.value = id
  await handleGetEpisode(id)
  document.getElementById(`modal-episode-${id}`).showModal()
}

async function handleGetEpisodes() {
  episodios.value = []
  totalPaginas.value = 0
  try {
    const response = await axios.get('https://rickandmortyapi.com/api/episode', {
      params: {
        page: paginaAtual.value,
      },
    })
    episodios.value = response.data.results
    totalPaginas.value = response.data.info.pages
  } catch (error) {
    console.error('Error fetching episodes:', error)
  }
}

async function handleGetEpisode(id) {
  episodioIndividual.value = null
  try {
    const response = await axios.get(`https://rickandmortyapi.com/api/episode/${id}`)
    episodioIndividual.value = response.data
    personagens.value = episodioIndividual.value.characters
  } catch (error) {
    console.error('Error fetching episode:', error)
  }
}

async function setPagination(novaPagina) {
  paginaAtual.value = novaPagina
  await handleGetEpisodes()
}

onMounted(async () => {
  await handleGetEpisodes()
})
</script>
