<template>
  <div id="app">
    <h1>VueJS carousel demo</h1>
    <EntranceComponent 
        :photo="['logo.png', 'logo.png', 'logo.png', 'logo.png', 'logo.png', 'logo.png','logo.png', 'logo.png', 'logo.png']" 
        height="60" 
        maxWidth="200"
        marg="auto" />
  </div>
</template>

<script>
import EntranceComponent from "./components/EntranceComponent";

export default {
  name: 'app',
  components: {
    EntranceComponent 
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 600px;
    margin: 60px auto;
}
</style>
