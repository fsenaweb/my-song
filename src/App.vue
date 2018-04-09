<template>
  <v-app class="white">
    <v-toolbar dark color="primary">
      <v-toolbar-title><router-link to="/" style="text-decoration: none" class="white--text">My Song</router-link></v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    <router-view></router-view>
    <v-footer :fixed="fixed" app>
      <span style="margin-left: 4vw">Vagalume © - Todos os Direitos Reservados</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [{
        icon: 'bubble_chart',
        title: 'Inspire'
      }],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  },
  name: 'App'
}
</script>
