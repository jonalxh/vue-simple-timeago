<template>
  <div id="app" class="App">
    <SimpleTimeAgo :date="twentyNineSeconds"></SimpleTimeAgo>
    <SimpleTimeAgo :date="yesterday"></SimpleTimeAgo>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      twentyNineSeconds: Date.now() - (29 * 1000),
      yesterday: Date.now() - (1 * 24 * 60 * 60 * 1000),
    }
  },
}
</script>

<style>
  body {
    margin: 1em;
  }
</style>
