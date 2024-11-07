<script setup lang="ts">
import { computed, ref } from 'vue'

const cheval = ref<string | null>(null)
const chat = ref<string | null>(null)
const filled = computed<boolean>(() => cheval.value !== null && chat.value !== null)

function submit(event: Event): void {
  event.preventDefault()
  if (filled.value) {
    alert(`Vous avez choisi la couleur ${cheval.value} pour le cheval et la couleur ${chat.value} pour le chat !`)
  }
}
</script>

<template>
  <form @submit="submit">
    De quelle couleur est le cheval blanc de Napoléon ?
    <div class="form-check">
      <input
        id="chevalBlanc"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="blanc"
      />
      <label class="form-check-label" for="chevalBlanc">Blanc</label>
    </div>
    <div class="form-check">
      <input
        id="chevalBrun"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="brun"
      />
      <label class="form-check-label" for="chevalBrun">Brun</label>
    </div>
    <div class="form-check">
      <input
        id="chevalNoir"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="noir"
      />
      <label class="form-check-label" for="chevalNoir">Noir</label>
    </div>
  </form>
  <form @submit="submit">
    De quelle couleur est le chat?
    <div class="form-check">
      <input
        id="chatrouge"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="Rouge"
      />
      <label class="form-check-label" for="chevalBlanc">Rouge</label>
    </div>
    <div class="form-check">
      <input
        id="chatjaune"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="Jaune"
      />
      <label class="form-check-label" for="chatjaune">Jaune</label>
    </div>
    <div class="form-check">
      <input
        id="chatvert"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="vert"
      />
      <label class="form-check-label" for="chatvert">Vert</label>
    </div>
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
  </form>
</template>
