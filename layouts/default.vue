<template>
  <v-app app dark>
  <v-navigation-drawer app>
  </v-navigation-drawer>

  <v-app-bar
    app

  >
    <v-app-bar-nav-icon></v-app-bar-nav-icon>
    <v-btn icon >
      <v-icon>mdi-arrow-left</v-icon>
    </v-btn>
    <v-toolbar-title>Title</v-toolbar-title>
  </v-app-bar>


  <!-- Sizes your content based upon application components -->
  <v-content>

    <!-- Provides the application the proper gutter -->
    <v-container fluid>

      <!-- If using vue-router -->
      <nuxt/>
    </v-container>
  </v-content>

  <v-footer app>
    <!-- -->
  </v-footer>
</v-app>
</template>

<script>
import { mdiArrowLeft } from '@mdi/js'; 
import {mapState} from 'vuex'
export default {
  computed: mapState(['user'])
}
</script>
