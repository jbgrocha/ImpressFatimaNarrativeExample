<template>
  <div id="app">
    <ImpressNarrative />
  </div>
</template>

<script>
import Vue from 'vue'
import ImpressNarrative from './components/ImpressNarrative.vue'
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

// Bootstrap css
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

// Install BootstrapVue
Vue.use(BootstrapVue)
// Optionally install the BootstrapVue icon components plugin
Vue.use(IconsPlugin)

export default {
  name: 'app',
  components: {
    ImpressNarrative
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
