<template>
  <div
    class="card p-1 bg-base-100 shadow-sm hover:shadow-lg hover:bg-base-300 transition-shadow duration-300 cursor-pointer"
    tabindex="0"
    role="button"
    @click="cardClick"
  >
    <avatar-group :personagens="props.personagens" />
    <div class="card-body">
      <h2 class="card-title">
        {{ titulo }}
        <badge-episode>
          {{ episodio }}
        </badge-episode>
      </h2>
      <div class="card-actions justify-end">
        <badge-air-date>
          {{ lancamento }}
        </badge-air-date>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  titulo: String,
  id: Number,
  episodio: String,
  lancamento: String,
  personagens: Array,
})

const emit = defineEmits(['card-click'])

function cardClick() {
  emit('card-click', props.id.toString())
}
</script>
