
<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>      
          <th> <!-- Position --> </th>
          <th> <!-- Logo --> </th>
          <th> <!-- Name --> </th>   
          
          <th>Form</th>
          <th>GP</th>
          <th>W</th>
          <th>D</th>
          <th>L</th>
          <th>GF</th>
          <th>GA</th>
          <th>GD</th>
          <th>Pts</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in standingsTable" :key="item.idStanding">
          <td>{{ item.intRank }}</td>
          <td>
            <v-avatar>
              <img :src="item.strTeamBadge" />
            </v-avatar>
          </td>
          <td>{{ item.strTeam }}</td>
          <td>{{ item.strForm }}</td>
          <td>{{ item.intPlayed }}</td>
          <td>{{ item.intWin }}</td>
          <td>{{ item.intDraw }}</td>
          <td>{{ item.intLoss }}</td>
          <td>{{ item.intGoalsFor }}</td>
          <td>{{ item.intGoalsAgainst }}</td>
          <td>{{ item.intGoalDifference }}</td>
          <td>{{ item.intPoints }}</td>
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