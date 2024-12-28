<script setup lang="ts">
import { computed, defineModel, defineProps, ref, watch, type PropType, onMounted } from 'vue'
import { QuestionState } from '@/utils/models'

const model = defineModel<QuestionState>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  answerDetail: { type: String, default: "Pas plus d'information sur la question." },
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>,
    required: true,
  },
})

const value = ref<string | null>(null)

function shuffleArray<T>(array: T[]): T[] {
  return array.sort(() => Math.random() - 0.5)
}

const shuffledOptions = ref<{ value: string; text: string }[]>([])

onMounted(() => {
  shuffledOptions.value = shuffleArray([...props.options])
})

const answerText = computed<string>(
  () => props.options.find((option) => option.value === props.answer)?.text ?? props.answer,
)

watch(model, (newModel) => {
  if (newModel === QuestionState.Submit) {
    model.value = value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong
  } else if (newModel === QuestionState.Empty) {
    value.value = null
  }
})

watch(
  value,
  (newValue) => {
    if (newValue === null) {
      model.value = QuestionState.Empty
    } else {
      model.value = QuestionState.Fill
    }
  },
  { immediate: true },
)
</script>

<template>
  <div>{{ props.text }}</div>

  <select
    v-model="value"
    :disabled="
      model === QuestionState.Submit ||
      model === QuestionState.Correct ||
      model === QuestionState.Wrong
    "
  >
    <option value="" disabled selected>Choisissez une réponse</option>

    <option v-for="option in shuffledOptions" :key="option.value" :value="option.value">
      {{ option.text }}
    </option>
  </select>

  <div v-if="model === QuestionState.Correct || model === QuestionState.Wrong">
    <p v-if="model === QuestionState.Correct" class="text-success">Juste !</p>
    <p v-else class="text-danger">Faux ! La réponse était : {{ answerText }}</p>
    <p class="blockquote-footer">{{ props.answerDetail }}</p>
  </div>
</template>

<style scoped>
.text-danger {
  color: rgb(255, 52, 52) !important;
}
.text-success {
  color: rgb(21, 255, 0) !important;
}
</style>
