<template>
<div id="app">
  <h1><router-link to="/" class="title">Title</router-link></h1>
  <router-view/>
  <div id="footer">
    <router-link to="/about">About</router-link>
  </div>
</div>
</template>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.title {
  padding: 10px;
  border-radius: 5px;
  color: inherit;
  text-decoration: inherit;
}
#footer {
  padding: 30px;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
