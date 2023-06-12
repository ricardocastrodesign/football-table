
<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">Name</th>
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