<template>
  <dialog :id="`modal-episode-${id}`" class="modal">
    <div class="modal-box">
      <form method="dialog">
        <button class="btn btn-sm btn-circle btn-ghost absolute right-2 top-2">✕</button>
      </form>
      <h3 class="text-lg font-bold pb-4">
        {{ episodio.name }}
        <badge-episode>{{ episodio.episode }}</badge-episode>
      </h3>
      <avatar-group :grupo="false" :exibir-todos="true" :personagens="props.personagens" />
      <p class="flex justify-end pt-4">
        <badge-air-date> {{ episodio.air_date }} </badge-air-date>
      </p>
    </div>
  </dialog>
</template>

<script setup>
const props = defineProps({
  episodio: Object,
  personagens: Array,
  id: String,
})

const emit = defineEmits(['pesquisar-episodio'])
</script>
