<template>
  <div id="nav">
    <router-link to="/"></router-link> 
    <router-link to="/about"></router-link>
  </div>
  <router-view />
</template>
<script>
export default {
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 10px 10px;
  display: flex;
  justify-content: space-between;
}

#nav:before {
  position: absolute;
  top: 70px;
  left: 20px;
  right: 20px;
  border-top: 1px solid silver;
  content: '';
}
  
#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
