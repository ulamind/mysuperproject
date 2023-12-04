<template>
  <div id="nav" v-if="!hideCard">
    <router-link to="/"><img src="./assets/logo.png"/></router-link> 
    <router-link to="/about"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"><path fill="black" d="M6 6a4 4 0 0 1 4-4h4a4 4 0 0 1 4 4v2h4a1 1 0 0 1 .986 1.164l-1.582 9.494A4 4 0 0 1 17.46 22H6.54a4 4 0 0 1-3.945-3.342L1.014 9.164A1 1 0 0 1 2 8h4V6Zm2 2h5a1 1 0 1 1 0 2H3.18l1.389 8.329A2 2 0 0 0 6.54 20h10.92a2 2 0 0 0 1.972-1.671L20.82 10H17a1 1 0 0 1-1-1V6a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v2Z"></path></svg></router-link>
  </div>
  <router-view />
</template>
<script>
export default {
  props: ['hideCard'],
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
