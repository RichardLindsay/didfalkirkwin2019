<template :if="gotData">
  <div id="app">
    <div
      class="home score"
      :class="{ is_us: isUs(match.matchesTeam.match[0].homeTeamNo) }"
    >{{ match.matchesTeam.match[0].homeTeamScore }}</div>

    <div
      class="away score"
      :class="{ is_us: isUs(match.matchesTeam.match[0].awayTeamNo) }"
    >{{ match.matchesTeam.match[0].awayTeamScore }}</div>

    <!-- <div
      class="home score"
      :class="{ is_us: isUs(match.results[0].idHomeTeam) }"
    >{{ match.results[0].intHomeScore }}</div>

    <div
      class="away score"
      :class="{ is_us: isUs(match.results[0].idAwayTeam) }"
    >{{ match.results[0].intAwayScore }}</div>-->
  </div>
</template>

<script>
import { setTimeout } from "timers";

export default {
  name: "app",
  data() {
    return {
      match: []
    };
  },

  methods: {
    isUs(team_number) {
      if (team_number == 343) {
        return true;
      } else {
        return false;
      }
    }
    // isUs(team_number) {
    //   if (team_number == "133838") {
    //     return true;
    //   } else {
    //     return false;
    //   }
    // }
  },

  computed: {
    // gotData() {
    //   return this.match.length;
    // }
  },

  mounted() {
    setTimeout(() => {
      //   fetch(
      //     "https://www.thesportsdb.com/api/v1/json/1/eventslast.php?id=133838"
      //   )
      //     .then(response => response.json())
      //     .then(data => {
      //       this.match = data;
      //     });
      // }, 2000);
      fetch(
        "https://www.footballwebpages.co.uk/fixtures-results.json?team=343&results=1&fixtures=0"
      )
        .then(response => response.json())
        .then(data => {
          this.match = data;
        });
    }, 2000);
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Rubik&display=swap");

* {
  box-sizing: border-box;
}

html,
body {
  margin: 0;
}

#app {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  height: 100vh;
  font-family: "Rubik";
  font-size: 88px;
}

.score {
  height: 50vh;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}

.score.is_us {
  background-color: #231f20;
  color: #fff;
}

@media only screen and (min-width: 850px) {
  #app {
    flex-direction: row;
    font-size: 130px;
  }

  .score {
    height: 100%;
    width: 50vw;
  }
}

@media only screen and (min-width: 1320px) {
  #app {
    font-size: 230px;
  }
}
</style>
