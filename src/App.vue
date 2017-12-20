<template>
  <div id="app">
    <Demo/>
  </div>
</template>

<script>
import Demo from './components/Demo'

export default {
  name: 'app',
  components: {
    Demo
  }
}
</script>

<style>
#app {
  padding: 40px;
}
</style>
