<script setup>
import { ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()

const id = route.params.id
const ordinateurs = JSON.parse(localStorage.getItem('ordinateurs')) || []

const ordinateur = ref({
  modele: '',
  processeur: '',
  memoire: 8,
  disque: 256,
  carteGraphique: '',
  photo: 'https://placehold.co/600x400?text=Ordinateur'
})

if (id) {
  const trouve = ordinateurs.find((o) => o.id === Number(id))

  if (trouve) {
    ordinateur.value = { ...trouve }
  }
}

const erreur = ref('')

function enregistrer() {
  if (!ordinateur.value.modele.trim() || !ordinateur.value.processeur.trim()) {
    erreur.value = 'Le modèle et le processeur sont obligatoires.'
    return
  }

  if (ordinateur.value.memoire <= 0 || ordinateur.value.disque <= 0) {
    erreur.value = 'La mémoire et le disque doivent être supérieurs à zéro.'
    return
  }

  if (id) {
    const index = ordinateurs.findIndex((o) => o.id === Number(id))

    if (index === -1) {
      erreur.value = 'Ordinateur introuvable.'
      return
    }

    ordinateurs[index] = { ...ordinateur.value }
  } else {
    ordinateurs.push({
      ...ordinateur.value,
      id: Date.now()
    })
  }

  localStorage.setItem('ordinateurs', JSON.stringify(ordinateurs))
  router.push('/ordinateurs')
}
</script>

<template>
  <main class="formulaire">
    <h1>{{ id ? 'Modifier un ordinateur' : 'Ajouter un ordinateur' }}</h1>

    <form @submit.prevent="enregistrer">
      <label>Modèle :</label>
      <input v-model="ordinateur.modele" type="text" required />

      <label>Processeur :</label>
      <input v-model="ordinateur.processeur" type="text" required />

      <label>Mémoire (Go) :</label>
      <input v-model.number="ordinateur.memoire" type="number" min="1" required />

      <label>Disque (Go) :</label>
      <input v-model.number="ordinateur.disque" type="number" min="1" required />

      <label>Carte graphique :</label>
      <input v-model="ordinateur.carteGraphique" type="text" />

      <label>Photo (URL) :</label>
      <input v-model="ordinateur.photo" type="url" />

      <p v-if="erreur" class="erreur">{{ erreur }}</p>

      <button type="submit">Enregistrer</button>
      <button type="button" @click="router.push('/ordinateurs')">
        Annuler
      </button>
    </form>
  </main>
</template>

<style scoped>
.formulaire {
  max-width: 550px;
  margin: 30px auto;
  padding: 20px;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 10px;
  cursor: pointer;
}

.erreur {
  color: red;
}
</style>