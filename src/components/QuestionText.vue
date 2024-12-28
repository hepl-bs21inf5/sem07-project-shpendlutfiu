<script setup lang="ts">
import { defineModel, defineProps, ref, watch } from 'vue'
import { QuestionState } from '@/utils/models'

const model = defineModel<QuestionState>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  answerDetail: { type: String, default: "Pas plus d'information sur la question." },
  placeholder: { type: String, default: 'veuillez noter quelque chose' },
})

const value = ref<string | null>(null)

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
    if (newValue === null || newValue === '') {
      model.value = QuestionState.Empty
    } else {
      model.value = QuestionState.Fill
    }
  },
  { immediate: true },
)
</script>

<template>
  {{ props.text }}
  <div>
    <label for="exampleFormControlInput" class="form-label"></label>
    <input
      id="props.id"
      v-model="value"
      class="form-control"
      :placeholder="props.placeholder"
      :disabled="
        model === QuestionState.Submit ||
        model === QuestionState.Correct ||
        model === QuestionState.Wrong
      "
    />
  </div>
  <div v-if="model === QuestionState.Correct || model === QuestionState.Wrong">
    <p v-if="model === QuestionState.Correct" class="text-success">Juste !</p>
    <p v-else class="text-danger">Faux ! La réponse était : {{ props.answer }}</p>
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
