<template>
 <div id="app">
   <UserProfile/>
 </div>
 
</template>

<script>
import UserProfile from "./components/UserProfile";

  export default {
    name: 'App',
    components:{UserProfile}
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
 
  color: #2c3e50;
  min-height: 100vh;;
  background-color: #F3F5FA;
}
</style>
