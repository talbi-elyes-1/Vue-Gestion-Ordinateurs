<script setup>
defineProps({ ordinateur: Object })
defineEmits(['modifier', 'supprimer'])
</script>

<template>
  <article class="carte">
    <img :src="ordinateur.photo" :alt="ordinateur.modele" />
      
  

    <div class="informations">
      <h2>{{ ordinateur.modele }}</h2>

      <p><strong>Processeur :</strong> {{ ordinateur.processeur }}</p>
      <p><strong>Mémoire :</strong> {{ ordinateur.memoire }} Go</p>
      <p><strong>Disque :</strong> {{ ordinateur.disque }} Go</p>
      <p><strong>Carte graphique :</strong> {{ ordinateur.carteGraphique }}</p>

      <button @click="$emit('modifier', ordinateur.id)">Modifier</button>
      <button @click="$emit('supprimer', ordinateur.id)">Supprimer</button>
    </div>
  </article>
</template>

<style scoped>
.carte {
  background: white;
  border-radius: 12px;
  padding: 16px;
  box-shadow: 0 2px 8px #0002;
}

.carte img {
  width: 100%;
  height: 160px;
  object-fit: cover;
  border-radius: 8px;
}

.carte button {
  margin: 5px;
  padding: 8px 12px;
  cursor: pointer;
}
</style>




