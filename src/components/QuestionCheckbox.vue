<script setup lang="ts">
import { computed, defineModel, defineProps, ref, watch, type PropType } from 'vue'
import { QuestionState } from '@/utils/models'

const model = defineModel<QuestionState>()

const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: {
    type: Array as PropType<string[]>,
    required: true,
  },
  answerDetail: { type: String, default: "Pas plus d'information sur la question." },
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>,
    required: true,
  },
})

const values = ref<string[]>([])

const answerText = computed<string>(() => {
  const correctAnswers = props.answer.map(
    (a) => props.options.find((option) => option.value === a)?.text ?? a,
  )
  return correctAnswers.join(', ')
})

watch(model, (newModel) => {
  if (newModel === QuestionState.Submit) {
    const isCorrect =
      values.value.length === props.answer.length &&
      values.value.every((val) => props.answer.includes(val))
    model.value = isCorrect ? QuestionState.Correct : QuestionState.Wrong
  } else if (newModel === QuestionState.Empty) {
    values.value = []
  }
})

// Watcher pour mettre à jour l'état de la question (remplie ou vide)
watch(
  values,
  (newValue) => {
    if (newValue.length === 0) {
      model.value = QuestionState.Empty
    } else {
      model.value = QuestionState.Fill
    }
  },
  { immediate: true },
)
</script>

<template>
  <div>
    <p>{{ props.text }}</p>
    <div v-for="option in props.options" :key="option.value" class="form-check">
      <input
        :id="`${props.id}-${option.value}`"
        v-model="values"
        class="form-check-input"
        type="checkbox"
        :name="props.id"
        :value="option.value"
        :disabled="
          model === QuestionState.Submit ||
          model === QuestionState.Correct ||
          model === QuestionState.Wrong
        "
      />
      <label class="form-check-label" :for="`${props.id}-${option.value}`">
        {{ option.text }}
      </label>
    </div>
    <div v-if="model === QuestionState.Correct || model === QuestionState.Wrong">
      <p v-if="model === QuestionState.Correct" class="text-success">Juste !</p>
      <p v-else class="text-danger">Faux ! La ou les bonnes réponses étaient : {{ answerText }}</p>
      <p class="blockquote-footer">{{ props.answerDetail }}</p>
    </div>
  </div>
</template>

<style scoped>
.text-danger {
  color: rgb(255, 52, 52)!important;
}
.text-success {
  color: rgb(21, 255, 0) !important;
}
</style>
