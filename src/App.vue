<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>|
      <router-link to="/about">About</router-link>
    </div>
    <router-view />

  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
}
.insertBox {
  background: #2c3e50;
  border: #42b983 solid 1px;
  position: absolute;
  top: 50%;
  left: 50%;
  color: white;
  transform: translate(-50%, -50%);
}
.insertBox p {
  text-align: left;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}
html,
body {
  height: 100%;
}
#nav {
  background: #2c3e50;
  float: left;
  width: 50px;
  height: 100%;
}

#nav a {
  font-weight: bold;
  color: #cccc;
  display: block;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
