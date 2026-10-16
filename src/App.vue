<template>
  <div id="app">
    <header>
      <h1>💻 Parc Informatique</h1>

      <nav>
        <RouterLink to="/ordinateurs">Liste des ordinateurs</RouterLink>
        <RouterLink to="/ordinateurs/ajouter">Ajouter un ordinateur</RouterLink>
      </nav>
    </header>

    <RouterView />
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f3f6fa;
  color: #222;
}

header {
  background: #123b63;
  color: white;
  padding: 20px;
  text-align: center;
}

nav {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 20px;
}

nav a {
  color: white;
  text-decoration: none;
  padding: 8px;
}

nav a:hover {
  text-decoration: underline;
}
</style>