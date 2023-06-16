<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        Premier League Table       
      </div>

      <v-spacer></v-spacer>

      <v-switch
        v-model="darkTheme"
        label="Light/Dark Mode"
        @change="toggleTheme"
      ></v-switch>
    </v-app-bar>

    <v-main>
      <FootballTable />
    </v-main>
  </v-app>
</template>

<script>
import FootballTable from "./components/FootballTable";

export default {
  name: "App",

  components: {
    FootballTable,
  },

  data: () => ({
    darkTheme: false,
  }),
  methods: {
    toggleTheme() {
      this.$vuetify.theme.dark = this.darkTheme;
    },
  },
};
</script>
