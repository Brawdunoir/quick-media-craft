<script setup>
import { useDebounceFn } from '@vueuse/core'
import { ref } from 'vue';

const movieTitle = defineModel()

const updated = ref('');
const debouncedFn = useDebounceFn((e) => {
  movieTitle.value = e.target.value;
  updated.value = e.target.value;
}, 500, { maxWait: 3000 })
</script>

<template>
  <div :class="[updated ? 'container' : 'container faded']">
    <label>{{ $t('manualMovieName.description') }}</label>
    <input :value="updated" @input="debouncedFn" type="text"
      :placeholder="movieTitle ?? $t('manualMovieName.inputPlaceholder')">
  </div>
</template>

<style scoped>
.container {
  display: flex;
  align-items: center;
  text-align: center;
  gap: var(--margin-bottom);
  width: 100%;
}

.faded {
  opacity: 0.6;
  transition: opacity 0.3s ease;

  &:hover {
    opacity: 1;
  }
}

label {
  margin-bottom: var(--margin-bottom);
}
</style>
