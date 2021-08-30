<template>
  <v-app>
    <v-app-bar
      app
      fixed
      elevation="5"
      color="secondary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="./assets/midari_studio_logo.png"
          transition="scale-transition"
          width="90"
        />

        <span class="mr-2">Midari Profile Studio</span>
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
    <v-footer class="footer" 
      color="secondary"
      
      elevation="5"
    >
      MPS v0.0.2 by Minzkraut - Send feedback via <a href="https://mnz.gg/discord" title="Minzkrauts Discord">Discord </a> - Icons made by <a href="https://www.freepik.com" title="Freepik">Freepik</a>
    </v-footer>
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

a, footer.footer a {
  margin: 0 5px;
  color: #52BD6F;
}
.v-color-picker__alpha {
  display: none;
}
.v-color-picker__hue {
  margin-bottom: 0 !important;
}

.footer {
  justify-content: center;
  font-size: 12px;
}
</style>
