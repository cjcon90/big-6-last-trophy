<template>
  <div id="app">
    <div class=" flex flex-wrap justify-center">
      <button
        v-for="(value, trophy) in filter"
        :key="trophy"
        class=" bg-green-500 m-2 p-2"
        :class="value ? 'opacity-100' : 'opacity-50'"
        @click="filterTrophy(trophy)"
      >
        {{ trophy }}
      </button>
    </div>
    <ClubTrophies class=" m-6" v-for="club in clubs" :key="club.name" :club="club" :logo="club.logo" :filter="filter" />
    <img :src="clubs.arsenal.logo" alt="" />
  </div>
</template>

<script>
import ClubTrophies from "./components/ClubTrophies.vue";

export default {
  name: "App",
  data() {
    return {
      filter: {
        "Champions League": true,
        "Premier League": true,
        "Europa League": true,
        "FA Cup": true,
        "League Cup": true,
        "Super Cup": true,
        "Community Shield": true,
      },
      clubs: {
        arsenal: {
          name: "Arsenal F.C.",
          logo: "arsenal.svg",
          trophies: {
            "Champions League": "",
            "Premier League": "May 15, 2004",
            "Europa League": "",
            "FA Cup": "Aug 1, 2020",
            "League Cup": "Apr 18, 1993",
            "Super Cup": "",
            "Community Shield": "Aug 29, 2020",
          },
        },
        chelsea: {
          name: "Chelsea F.C.",
          logo: "chelsea.svg",
          trophies: {
            "Champions League": "May 19, 2012",
            "Premier League": "May 21, 2017",
            "Europa League": "May 29, 2019",
            "FA Cup": "May 19, 2018",
            "League Cup": "Mar 1, 2015",
            "Super Cup": "Aug 28, 1998",
            "Community Shield": "Aug 9, 2009",
          },
        },
        liverpool: {
          name: "Liverpool F.C.",
          logo: "liverpool.svg",
          trophies: {
            "Champions League": "Jun 1, 2019",
            "Premier League": "Jul 26, 2020",
            "Europa League": "May 16, 2001",
            "FA Cup": "May 13, 2006",
            "League Cup": "Feb 26, 2012",
            "Super Cup": "Aug 14, 2019",
            "Community Shield": "Aug 13, 2006",
          },
        },
        mancity: {
          name: "Manchester City",
          logo: "mancity.svg",
          trophies: {
            "Champions League": "",
            "Premier League": "May 12, 2019",
            "Europa League": "",
            "FA Cup": "May 18, 2019",
            "League Cup": "Mar 1, 2020",
            "Super Cup": "",
            "Community Shield": "Aug 4, 2019",
          },
        },
        manutd: {
          name: "Manchester United",
          logo: "manutd.svg",
          trophies: {
            "Champions League": "May 21, 2008",
            "Premier League": "May 19, 2013",
            "Europa League": "May 24, 2017",
            "FA Cup": "May 21, 2016",
            "League Cup": "Feb 26, 2017",
            "Super Cup": "Nov 19, 1991",
            "Community Shield": "Aug 7, 2016",
          },
        },
        spurs: {
          name: "Tottenham Hotspurs",
          logo: "spurs.svg",
          trophies: {
            "Champions League": "",
            "Premier League": "Apr 29, 1961",
            "Europa League": "May 23, 1984",
            "FA Cup": "May 18, 1991 14:",
            "League Cup": "Feb 24, 2008",
            "Super Cup": "",
            "Community Shield": "Aug 10, 1991",
          },
        },
      },
    };
  },
  components: {
    ClubTrophies,
  },
  methods: {
    filterTrophy(trophy) {
      this.filter[trophy] = !this.filter[trophy];
    },
  },
};
</script>

<style lang="scss"></style>
