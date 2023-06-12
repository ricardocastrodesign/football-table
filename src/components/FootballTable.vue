<template>
  <div>
    <h1>Premier League Standings</h1>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "VueFootballTable",

  data() {
    return {};
  },

  mounted() {
    this.getStandings();
  },

  methods: {
    getStandings() {
      axios
        .get(
          "https://www.thesportsdb.com/api/v1/json/3/lookuptable.php?l=4328&s=2020-2021"
        )
        .then((response) => {
          console.log(response);
        });
    },
  },
};
</script>

<style lang="scss" scoped>
</style>