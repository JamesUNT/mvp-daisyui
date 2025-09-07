<template>
  <div v-if="props.grupo" class="avatar-group -space-x-6">
    <div
      class="avatar"
      v-for="(personagem, index) in props.exibirTodos ? props.personagens : personagensPrincipais"
      :key="index"
    >
      <div class="w-12">
        <img :src="getImagem(personagem)" />
      </div>
    </div>
    <div
      v-if="!props.exibirTodos && contagemPersonagensSecundarios >= 5"
      class="avatar avatar-placeholder"
    >
      <div class="bg-neutral text-neutral-content w-12">
        <span>+{{ contagemPersonagensSecundarios }}</span>
      </div>
    </div>
  </div>
  <div v-else>
    <div
      class="avatar"
      v-for="(personagem, index) in props.exibirTodos ? props.personagens : personagensPrincipais"
      :key="index"
    >
      <div class="w-12 rounded-full ring-2 ring-success">
        <img :src="getImagem(personagem)" />
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  grupo: { type: Boolean, default: true },
  exibirTodos: { type: Boolean, default: false },
  personagens: { type: Array, default: () => [] },
})

const personagensPrincipais = computed(() => {
  return props.personagens.length > 5 ? [...props.personagens.slice(0, 5)] : props.personagens.value
})

const contagemPersonagensSecundarios = computed(() => {
  return props.personagens.length > 5 ? props.personagens.length - 5 : 0
})

const getImagem = (url) => {
  const newUrl = url.replace(
    'https://rickandmortyapi.com/api/character/',
    `https://rickandmortyapi.com/api/character/avatar/`,
  )
  return `${newUrl}.jpeg`
}
</script>
