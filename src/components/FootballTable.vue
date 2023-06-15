
<template>
  <v-container fluid>
    <v-simple-table class="elevation-1 v-table--mobile">
      <template v-slot:default>
        <thead>
          <tr>
            <th><!-- Position --></th>
            <th><!-- Logo --></th>
            <th><!-- Name --></th>

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
            <td>{{ item.intRank | twoDigits }}</td>
            <td>
              <v-avatar size="32">
                <img :src="item.strTeamBadge" />
              </v-avatar>
            </td>
            <td>{{ item.strTeam }}</td>
            <td>
              <div class="form-icons">
                <v-icon
                  v-for="(char, index) in item.strForm"
                  :key="index"
                  :color="getIconBgColor(char)"
                >
                  {{ getIcon(char) }}
                </v-icon>
              </div>
            </td>
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
  </v-container>
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
  filters: {
    twoDigits(value) {
      return value.toString().padStart(2, "0");
    },
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
        });
    },
    getIcon(char) {
      if (char === "W") {
        return "mdi-checkbox-marked-circle";
      } else if (char === "L") {
        return "mdi-close-circle";
      }
      return "mdi-minus-circle";
    },

    getIconBgColor(char) {
      if (char === "W") {
        return "green";
      } else if (char === "L") {
        return "red";
      }
      return "grey";
    },
  },
};
</script>

<style lang="scss" scoped>
.form-icons {
  display: flex;
  flex-direction: row;
  align-items: center;
}
@media screen and (max-width: 720px) {
  .v-table--mobile {
    display: block;
    overflow-x: auto;
    white-space: nowrap;
  }


  .v-table--mobile thead th:nth-child(3),
  .v-table--mobile tbody td:nth-child(3) {
    position: sticky;
    left: 0;
    background-color: #fff;
    z-index: 1;
  }
}
</style>