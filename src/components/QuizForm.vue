<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from './QuestionText.vue'
import QuestionCheckbox from './QuestionCheckbox.vue'
import { QuestionState } from '@/utils/models'

const questionStates = ref<QuestionState[]>([])
const submitted = computed<boolean>(() =>
  questionStates.value.every(
    (state) => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
)

const score = computed<number>(
  () => questionStates.value.filter((state) => state === QuestionState.Correct).length,
)
const totalScore = computed<number>(() => questionStates.value.length)

const filled = computed<boolean>(() =>
  questionStates.value.every((state) => state === QuestionState.Fill),
)
function submit(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Submit)
}
function reset(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Empty)
}
</script>

<template>
  <form @submit="submit">
    <QuestionRadio
      v-model="questionStates[0]"
      answer="blanc"
      id="cheval"
      text="De quelle couleur est le cheval blanc de Napoléon ?"
      :options="[
        { value: 'blanc', text: 'Blanc' },
        { value: 'brun', text: 'Brun' },
        { value: 'noir', text: 'Noir' },
        { value: 'gris', text: 'Gris' },
      ]"
    />

    <QuestionRadio
      v-model="questionStates[1]"
      answer="jaune"
      id="chat"
      text="De quelle couleur est le chat?"
      :options="[
        { value: 'rouge', text: 'Rouge' },
        { value: 'jaune', text: 'Jaune' },
        { value: 'vert', text: 'vert' },
        { value: 'noir', text: 'Noir' },
      ]"
    />

    <QuestionRadio
      v-model="questionStates[2]"
      answer="4"
      id="carre"
      text="Combien de côtés a un carré?"
      :options="[
        { value: '1', text: '1' },
        { value: '2', text: '2' },
        { value: '3', text: '3' },
        { value: '4', text: '4' },
      ]"
    />
    <QuestionText
      id="patte"
      v-model="questionStates[3]"
      answer="4"
      text="Combien de pattes a un chat ?"
    />

    <QuestionText
      id="branche"
      v-model="questionStates[4]"
      answer="4"
      text="Combien il y a de branches au bs1 ?"
      placeholder="veuillez noter un nombre"
    />
    <p></p>
    <div>Réponses correctes : {{ questionStates }}</div>
    <p></p>
    <div>Debug états : {{ questionStates }}</div>
    <p></p>
    <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div>
    <p></p>
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <p></p>

    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
  </form>
</template>
