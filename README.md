# Gestion d’un parc informatique

## Présentation

Cette application web permet de gérer un parc informatique à l’aide de Vue.js 3. Elle permet d’afficher, d’ajouter, de modifier et de supprimer des ordinateurs.

## Fonctionnalités

* Affichage de la liste des ordinateurs.
* Ajout d’un nouvel ordinateur.
* Modification des informations d’un ordinateur.
* Suppression avec confirmation.
* Recherche par modèle ou processeur.
* Tri des ordinateurs par mémoire RAM.
* Affichage du nombre total d’ordinateurs.
* Validation des champs obligatoires.
* Sauvegarde des données dans le navigateur avec `localStorage`.
* Conservation des données après actualisation de la page.

## Technologies utilisées

* Vue.js 3
* JavaScript
* Vue Router
* HTML5
* CSS3
* Vite
* LocalStorage

## Structure du projet

```text
src/
├── assets/
│   └── images/
├── components/
│   └── OrdinateurCard.vue
├── data/
│   └── ordinateurs.js
├── router/
│   └── index.js
├── views/
│   ├── ListeOrdinateurs.vue
│   └── EditOrdinateur.vue
├── App.vue
└── main.js
```

## Installation et lancement

### 1. Cloner le projet

```bash
git clone https://github.com/talbi-elyes-1/Vue-Gestion-Ordinateurs.git
```

### 2. Accéder au dossier

```bash
cd Vue-Gestion-Ordinateurs
```

### 3. Installer les dépendances

```bash
npm install
```

### 4. Lancer l’application

```bash
npm run dev
```

Ouvrir ensuite l’adresse locale affichée dans le terminal, généralement `http://localhost:5173/`.

Sous Windows PowerShell, si la commande `npm` rencontre un problème d’exécution, utiliser `npm.cmd` à la place.

## Navigation

* `/ordinateurs` : afficher la liste des ordinateurs.
* `/ordinateurs/ajouter` : ajouter un ordinateur.
* `/ordinateurs/modifier/:id` : modifier un ordinateur existant.

## Stockage des données

Les informations sont enregistrées dans le `localStorage` du navigateur. Elles restent disponibles après l’actualisation de la page sur le même navigateur.

## Auteur

Projet réalisé dans le cadre d’un TP Vue.js 3 — Gestion d’un parc informatique.
