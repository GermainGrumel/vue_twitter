<template>

<div id="app">
  <UserProfile/>
  </div>
</template>

<script>
import UserProfile from "./components/UserProfile.vue";

export default {
  name: 'App',
  components:{UserProfile},
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #F3F5FA;
  min-height: 100vh;
  color: #2C3E50;
}
</style>
