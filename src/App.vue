<template>
  <v-app>
    <v-content>
      <Treeview />
      <Range />
    </v-content>
  </v-app>
</template>

<script>
import Treeview from './components/Treeview';
import Range from './components/Range';

export default {
  name: 'App',
  components: {
    Treeview,
    Range,
  },
  data () {
    return {
      //
    }
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Rubik:400,500,700');

  * {
    font-family: 'Rubik', 'Roboto', sans-serif;
  }

  body {
    color: #1d1e1e;
    background-color: #fff;
    box-sizing: border-box;
  }
</style>

