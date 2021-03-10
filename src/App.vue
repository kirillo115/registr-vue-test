<template>
  <div id="app">
    <component :is="layout">
      <router-view/>
    </component>
  </div>
</template>

<script>
import EmptyLayout from './layoyts/EmptyLayout'
import MainLayout from './layoyts/MainLayout'


export default {
  name: 'app',
  data() {
    return {
      info: ''
    }
  },

  components: {
     EmptyLayout,
     MainLayout,
  },

  computed: {
    layout() {
      return (this.$route.meta.layout || 'empty') + '-layout'
    }
  },
}
</script>

<style lang="scss">
@import '~normalize.css';
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap');
@import '~materialize-css/dist/css/materialize.min.css'
</style>
