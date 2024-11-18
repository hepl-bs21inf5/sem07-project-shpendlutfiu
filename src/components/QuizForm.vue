<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'

const cheval = ref<string | null>(null)
const chat = ref<string | null>(null)
const carre = ref<string | null>(null)
const filled = computed<boolean>(
  () => cheval.value !== null && chat.value !== null && carre.value !== null,
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
  cheval.value = null
  chat.value = null
  carre.value = null
}
</script>

<template>
  <form @submit="submit">
    <QuestionRadio
      id="cheval"
      v-model="cheval"
      text="De quelle couleur est le cheval blanc de Napoléon ?"
      :options="[
        { value: 'blanc', text: 'Blanc' },
        { value: 'brun', text: 'Brun' },
        { value: 'noir', text: 'Noir' },
        { value: 'gris', text: 'Gris' },
      ]"
    />
  </form>
  <form @submit="submit">
    <QuestionRadio
      id="chat"
      v-model="chat"
      text="De quelle couleur est le chat?"
      :options="[
        { value: 'rouge', text: 'Rouge' },
        { value: 'jaune', text: 'Jaune' },
        { value: 'vert', text: 'vert' },
        { value: 'noir', text: 'Noir' },
      ]"
    />
  </form>
  <form @submit="submit">
    <QuestionRadio
      id="carre"
      v-model="carre"
      text="Combien de côtés a un carré?"
      :options="[
        { value: '1', text: '1' },
        { value: '2', text: '2' },
        { value: '3', text: '3' },
        { value: '4', text: '4' },
      ]"
    />
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>

    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
  </form>
</template>
