<script setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'
import OrdinateurCard from '../components/OrdinateurCard.vue'
import { ordinateursExemple } from '../data/ordinateurs'

const router = useRouter()

// Charger les ordinateurs enregistrés
const ordinateursEnregistres = JSON.parse(
  localStorage.getItem('ordinateurs')
)

const ordinateurs = ref(
  ordinateursEnregistres || ordinateursExemple
)

// Mettre à jour les chemins des photos
ordinateurs.value.forEach((ordinateur) => {
  const ordinateurExemple = ordinateursExemple.find(
    (o) => o.id === ordinateur.id
  )

  if (ordinateurExemple) {
    ordinateur.photo = ordinateurExemple.photo
  }
})

// Enregistrer les données mises à jour
localStorage.setItem('ordinateurs', JSON.stringify(ordinateurs.value))

const recherche = ref('')
const triMemoire = ref(false)

const listeFiltree = computed(() => {
  let resultat = ordinateurs.value.filter((ordinateur) =>
    ordinateur.modele.toLowerCase().includes(recherche.value.toLowerCase()) ||
    ordinateur.processeur.toLowerCase().includes(recherche.value.toLowerCase())
  )

  if (triMemoire.value) {
    resultat.sort((a, b) => b.memoire - a.memoire)
  }

  return resultat
})

function supprimerOrdinateur(id) {
  if (confirm('Voulez-vous vraiment supprimer cet ordinateur ?')) {
    ordinateurs.value = ordinateurs.value.filter(
      (ordinateur) => ordinateur.id !== id
    )

    localStorage.setItem('ordinateurs', JSON.stringify(ordinateurs.value))
  }
}
</script>

<template>
  <main class="page">
    <h1>Gestion du parc informatique</h1>

    <p>Nombre d'ordinateurs : {{ ordinateurs.length }}</p>

    <div class="outils">
      <input
        v-model="recherche"
        type="text"
        placeholder="Rechercher un modèle ou un processeur"
      />

      <button @click="triMemoire = !triMemoire">
        Trier par mémoire
      </button>

      <button @click="router.push('/ordinateurs/ajouter')">
        Ajouter un ordinateur
      </button>
    </div>

    <section class="liste">
      <OrdinateurCard
        v-for="ordinateur in listeFiltree"
        :key="ordinateur.id"
        :ordinateur="ordinateur"
        @modifier="router.push('/ordinateurs/modifier/' + $event)"
        @supprimer="supprimerOrdinateur"
      />
    </section>

    <p v-if="listeFiltree.length === 0">
      Aucun ordinateur trouvé.
    </p>
  </main>
</template>

<style scoped>
.page {
  max-width: 1200px;
  margin: auto;
  padding: 25px;
}

h1 {
  color: #123b63;
}

.outils {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin: 20px 0;
}

input,
button {
  padding: 10px;
}

button {
  cursor: pointer;
}

.liste {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
</style>
