
<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
        <!-- Remove Text-->
          <th class="text-left">Position</th>
          <th class="text-left">Logo</th>
          <th class="text-left">Name</th>
        <!-- End Remove Text -->

          <th class="text-left">Form</th>
          <th class="text-left">GP</th>
          <th class="text-left">W</th>
          <th class="text-left">D</th>
          <th class="text-left">L</th>
          <th class="text-left">GF</th>
          <th class="text-left">GA</th>
          <th class="text-left">GD</th>
          <th class="text-left">Pts</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in standingsTable" :key="item.idStanding">
          <td>{{ item.strTeam }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>



<script>
import axios from "axios";

export default {
  name: "VueFootballTable",

  data() {
    return {
      standingsTable: null,
    };
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
          this.standingsTable = response.data.table;

          console.log(response);
        });
    },
  },
};
</script>

<style lang="scss" scoped>
</style>