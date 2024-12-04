<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from './QuestionText.vue'
import QuestionCheckbox from './QuestionCheckbox.vue'

const correctAnswers = ref<boolean[]>([])
const cheval = ref<string | null>(null)
const reponse = ref<string | null>(null)
const chat = ref<string | null>(null)
const carre = ref<string | null>(null)
const branches = ref<string | null>(null)
const score = computed<number>(() => correctAnswers.value.filter((value) => value).length)
const totalScore = 5
const filled = computed<boolean>(
  () =>
    cheval.value !== null &&
    chat.value !== null &&
    carre.value !== null &&
    reponse.value !== '' &&
    branches.value !== '',
)

function submit(event: Event): void {
  event.preventDefault()
  let score = 0
  let scoremax = 0
  if (filled.value) {
    if (cheval.value == 'blanc') {
      score += 1
    }
    scoremax += 1

    if (chat.value == 'jaune') {
      score += 1
    }
    scoremax += 1

    if (carre.value == '4') {
      score += 1
    }
    scoremax += 1
    if (reponse.value == '4') {
      score += 1
    }
    scoremax += 1
    if (branches.value == '4') {
      score += 1
    }
    scoremax += 1
    if (score == scoremax) {
      alert(`vous avez fait un sans faute !!!`)
    } else {
      alert(
        `Vous avez choisi la couleur ${cheval.value} pour le cheval, la couleur ${chat.value} pour le chat, et ${carre.value} nombre de côté(s) pour le carré! Vous avez ${score} bonne(s) réponse(s)!`,
      )
    }
  }
}
function reset(event: Event): void {
  event.preventDefault()
}
</script>

<template>
  <form @submit="submit">
    <QuestionRadio
      v-model="correctAnswers[0]"
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
      v-model="correctAnswers[1]"
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
      v-model="correctAnswers[2]"
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
      v-model="correctAnswers[3]"
      answer="4"
      text="Combien de pattes a un chat ?"
    />

    <QuestionText
      id="branche"
      v-model="correctAnswers[4]"
      answer="4"
      text="Combien il y a de branches au bs1 ?"
      placeholder="veuillez noter un nombre"
    />
    <p></p>
    <div>Réponses correctes : {{ correctAnswers }}</div>
    <div>Score : {{ score }} / {{ totalScore }}</div>
    <p></p>
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <p></p>

    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
  </form>
</template>
