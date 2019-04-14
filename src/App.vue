<template>
  <main>
    <div id="app">
      <navi></navi>
      <router-view/>
    </div>
  </main>
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

*, *::before, *::after {
  margin: 0;
  box-sizing: border-box;
}

#app {
  font-family: 'Avenir', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: $dark;
  display: flex;
  width: 100%;
}

body::-webkit-scrollbar {
  width: 0;
}

.animate {
  transition-delay: .25s;
  transition-duration: 1s;
  transition-timing-function: ease-in;
}
 
.slide-up {
  opacity: 0;
}
 
.slide-up.animate-active {
  opacity: 1;
}

</style>
