<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Clock</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
body {
  color: #d5d5d5;
  background-color: #2c3e50;
}

#app {
  font-family: Avenir, Helvetica, Arial, monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
