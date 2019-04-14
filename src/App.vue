<template>
  <div id="app">
    <navi></navi>
    <router-view/>
  </div>
</template>

<script>
import navi from '@/components/menu'

export default {
  components: {
    navi
  }
}
</script>


<style lang="scss">

$dark: #1d2b3b;
$gray: #ebf0f4;
$blue: #0c57fb;

body {
  margin: 0;
}

html {
  overflow-x: hidden;
}

#app {
  font-family: 'Avenir', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: $dark;
}

body::-webkit-scrollbar {
  width: 0;
}


</style>
