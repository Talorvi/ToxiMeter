<template>
  <div id="app">
    <div class="title">ToxiMeter</div>
    <ToxicMeter />
  </div>
</template>

<script>
import ToxicMeter from './components/ToxicMeter.vue'

export default {
  name: 'App',
  components: {
    ToxicMeter
  }
}
</script>

<style>
body {
  background-color: #2c3e50;
  color: #EEE1B3;
  /*position:fixed;*/
  width: 100%;
  margin: 0;
  height: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 64px;
  margin-left: 8px;
  margin-right: 8px;
  height: 100%;
}
.title {
  font-family: 'Righteous', cursive;
  font-size: 96px;
  margin-bottom: 60px;
  margin-left: auto;
  margin-right: auto;
}

@media only screen and (max-width: 1000px) {
  .title {
    font-size: 48px;
    margin-bottom: 32px;
  }
  #app {
    margin-top: 32px;
    overflow: scroll;
  }
  body {
    overflow: scroll;
  }
}
</style>
