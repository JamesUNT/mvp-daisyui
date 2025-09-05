<template>
  <div class="card bg-base-100 shadow-sm">
    <div class="avatar-group -space-x-6">
      <div class="avatar" v-for="(personagem, index) in personagensPrincipais" :key="index">
        <div class="w-12">
          <img :src="getImagem(personagem)" />
        </div>
      </div>
      <div v-if="personagens.length > 5" class="avatar avatar-placeholder">
        <div class="bg-neutral text-neutral-content w-12">
          <span>+{{ personagens.length }}</span>
        </div>
      </div>
    </div>
    <div class="card-body">
      <h2 class="card-title">
        {{ titulo }}
        <div class="badge badge-secondary">{{ episodio }}</div>
      </h2>
      <div class="card-actions justify-start">
        <div class="badge badge-outline">{{ lancamento }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  titulo: String,
  episodio: String,
  lancamento: String,
  personagens: Array,
})

const personagensPrincipais = computed(() => {
  return props.personagens.length > 5 ? [...props.personagens.slice(0, 5)] : props.personagens
})

const getImagem = (url) => {
  const newUrl = url.replace(
    'https://rickandmortyapi.com/api/character/',
    `https://rickandmortyapi.com/api/character/avatar/`,
  )
  return `${newUrl}.jpeg`
}
</script>
