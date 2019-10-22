<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif; -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; text-align: center; color: #2c3e50;
  $i: 0;
  @while $i < 250 {
    $i: $i + 5;
    .mt#{$i}{margin-top: #{$i}px};
  }
}
</style>
