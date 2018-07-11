<template>
<div id="app">
  <h1><router-link to="/" class="title">顺火暖工具箱</router-link></h1>
  <div class="content">
    <router-view />
  </div>
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
  height: 100vh;
  display: flex;
  flex-direction: column;
}
.title {
  padding: 10px;
  border-radius: 5px;
  color: inherit;
  text-decoration: inherit;
}
.content {
  display: flex;
  margin-left: 200px;
  margin-right: 200px;
  flex: 1 1 auto;
}
#footer {
  padding: 30px;
  flex: 0 0 auto;
  justify-content: flex-end;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
