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
        <v-toolbar-title>Calculator</v-toolbar-title>
      </div>
    </v-app-bar>

    <v-main>
      <Calculator/>
    </v-main>
  </v-app>
</template>

<script>
import Calculator from './components/Calculator';

export default {
  name: 'App',

  components: {
    Calculator,
  },

  data: () => ({

  }),
};
</script>
