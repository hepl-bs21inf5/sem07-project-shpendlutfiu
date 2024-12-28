<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import { QuestionState } from '@/utils/models'

const questionStates = ref<QuestionState[]>([])

const score = computed(
  () => questionStates.value.filter((state) => state === QuestionState.Correct).length,
)
const totalScore = computed(() => questionStates.value.length)

const filled = computed(() => questionStates.value.every((state) => state !== QuestionState.Empty))

const submitted = computed<boolean>(() =>
  questionStates.value.every(
    (state) => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
)

const questions = ref<{ question: string; correct_answer: string; incorrect_answers: string[] }[]>(
  [],
)

fetch('https://opentdb.com/api.php?amount=10&type=multiple')
  .then((response) => response.json())
  .then((data) => {
    questions.value = data.results
    questionStates.value = Array(questions.value.length).fill(QuestionState.Empty)
  })

function submit(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Submit)
}
function reset(event: Event): void {
  event.preventDefault()

  questionStates.value = Array(questions.value.length).fill(QuestionState.Empty)
}
</script>

<template>
  <form @submit="submit">
    <QuestionRadio
      v-for="(question, index) in questions"
      :id="`question-${index}`"
      :key="index"
      v-model="questionStates[index]"
      :answer="question.correct_answer"
      :text="question.question"
      :options="[
        { value: question.correct_answer, text: question.correct_answer },
        ...question.incorrect_answers.map((answer) => ({
          value: answer,
          text: answer,
        })),
      ]"
    />

    <p></p>
    <div>Réponses correctes : {{ questionStates }}</div>
    <br />
    <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div>
    <br />
    <div v-if="submitted && score === totalScore">Vous avez fait un sans faute, bravo !</div>
    <br />
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <p></p>
    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
  </form>
</template>
