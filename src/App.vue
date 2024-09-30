<template>
  <nav>
    <router-link class="link" to="/">Задачи</router-link> |
    <router-link class="link" to="/about">О сайте</router-link>
  </nav>
  <router-view/>
</template>

<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 1%;
}

nav {
  display: flex;
  justify-content: center;
  padding: 1%;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  margin: 0 1%;

}

.link {
  text-decoration: none;
}

nav a.router-link-exact-active {
  color: #a0d3ff;

}
</style>
