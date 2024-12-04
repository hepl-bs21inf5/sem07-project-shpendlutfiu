<script setup lang="ts">
import { defineModel, defineProps, ref, watch, type PropType } from 'vue'

const model = defineModel<boolean | null>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  placeholder: { type: String, default: 'veuillez noter quelque chose' },
})

const value = ref<string | null>(null)

watch(
  value,
  (newValue) => {
    model.value = newValue === props.answer
  },
  { immediate: true },
)
</script>

<template>
  {{ props.text }}
  <div>
    <label for="exampleFormControlInput" class="form-label"></label>
    <input id="props.id" v-model="value" class="form-control" :placeholder="props.placeholder" />
  </div>
</template>
