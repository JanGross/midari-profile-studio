<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <span class="mr-2">Midari Profile Designer</span>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://mnz.gg"
        target="_blank"
        text
      >
        <span class="mr-2">mnz.gg</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Designer/>
    </v-main>
  </v-app>
</template>

<script>
import Designer from './components/Designer';

export default {
  name: 'App',

  components: {
    Designer,
  },

  data: () => ({
  }),
};
</script>
<style>
.v-color-picker__alpha {
  display: none;
}
.v-color-picker__hue {
  margin-bottom: 0 !important;
}
</style>
