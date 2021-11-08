<template>
  <div id="app">
    <meteo></meteo>
  </div>
</template>

<script>
import Meteo from './components/Meteo'

export default {
  name: 'App',
  components: {
    'meteo' : Meteo
  }
}
</script>

<style>
 body{
   background: #43c6ac;
   background: linear-gradient(to right, #de14ed, #14b429);
 }
</style>
