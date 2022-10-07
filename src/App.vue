<template>
  <main class='grid'>
    <pwd-generator/>
  </main>
</template>

<script>
import pwdGenerator from './components/pwdGenerator.vue'

export default {
  name: 'App',
  components: {
    pwdGenerator
  }
}
</script>

<style>
body {
  background: #170f1e;
}
</style>
