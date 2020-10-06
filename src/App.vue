<template>
  <div id="app" class="bg-green-700 min-h-screen" style="fontFamily: 'Roboto', sans-serif;">
    <header>
      <h1 class="text-center uppercase text-gray-100 text-2xl md:text-3xl lg:text-4xl py-10 lg:py-16 px-4 font-bold leading-10">
        Last Trophy of the Big 6
      </h1>
    </header>
    <div class="bg-gray-100 mx-auto py-8">
      <p class="text-center text-green-700 uppercase text-xl md:text-2xl block mb-4">Filter by <i class="fas fa-trophy"></i></p>
      <div class=" flex flex-wrap justify-center gap-2">
        <button
          v-for="(value, trophy) in filter"
          :key="trophy"
          class=" bg-green-700 py-2 px-4 text-sm sm:text-md md:text-lg text-gray-100 border-green-600 border-2"
          :class="value ? 'opacity-100 font-bold' : 'opacity-50'"
          @click="filterTrophy(trophy)"
        >
          {{ trophy }}
        </button>
      </div>
    </div>
    <div class="flex flex-wrap sm:gap-8 sm:py-8">
      <ClubTrophies v-for="club in clubs" :key="club.name" :club="club" :logo="club.logo" :filter="filter" />
    </div>
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
        "Europa League": true,
        "Premier League": true,
        "FA Cup": true,
        "League Cup": true,
        "Super Cup": true,
        "Community Shield": true,
      },
      clubs: {
        arsenal: {
          name: "Arsenal F.C.",
          logo: "arsenal.svg",
          colorPrimary: "#ef0107",
          colorSecondary: "#fefefe",
          trophies: {
            "Champions League": "",
            "Premier League": "May 15, 2004",
            "Europa League": "",
            "FA Cup": "Aug 1, 2020",
            "League Cup": "Apr 18, 1993",
            "Super Cup": "",
            "Community Shield": "Aug 29, 2020",
          },
          expanded: false,
        },
        chelsea: {
          name: "Chelsea F.C.",
          logo: "chelsea.svg",
          colorPrimary: "#034694",
          colorSecondary: "#fefefe",
          trophies: {
            "Champions League": "May 19, 2012",
            "Premier League": "May 21, 2017",
            "Europa League": "May 29, 2019",
            "FA Cup": "May 19, 2018",
            "League Cup": "Mar 1, 2015",
            "Super Cup": "Aug 28, 1998",
            "Community Shield": "Aug 9, 2009",
          },
          expanded: false,
        },
        liverpool: {
          name: "Liverpool F.C.",
          logo: "liverpool.svg",
          colorPrimary: "#d00027",
          colorSecondary: "#fefefe",
          trophies: {
            "Champions League": "Jun 1, 2019",
            "Premier League": "Jul 26, 2020",
            "Europa League": "May 16, 2001",
            "FA Cup": "May 13, 2006",
            "League Cup": "Feb 26, 2012",
            "Super Cup": "Aug 14, 2019",
            "Community Shield": "Aug 13, 2006",
          },
          expanded: false,
        },
        mancity: {
          name: "Manchester City",
          logo: "mancity.svg",
          colorPrimary: "#6caddf",
          colorSecondary: "#fefefe",
          trophies: {
            "Champions League": "",
            "Premier League": "May 12, 2019",
            "Europa League": "",
            "FA Cup": "May 18, 2019",
            "League Cup": "Mar 1, 2020",
            "Super Cup": "",
            "Community Shield": "Aug 4, 2019",
          },
          expanded: false,
        },
        manutd: {
          name: "Manchester United",
          logo: "manutd.svg",
          colorPrimary: "#df1b1f",
          colorSecondary: "#fefefe",
          trophies: {
            "Champions League": "May 21, 2008",
            "Premier League": "May 19, 2013",
            "Europa League": "May 24, 2017",
            "FA Cup": "May 21, 2016",
            "League Cup": "Feb 26, 2017",
            "Super Cup": "Nov 19, 1991",
            "Community Shield": "Aug 7, 2016",
          },
          expanded: false,
        },
        spurs: {
          name: "Tottenham Hotspurs",
          logo: "spurs.svg",
          colorPrimary: "#efefef",
          colorSecondary: "#0a1c56",
          trophies: {
            "Champions League": "",
            "Premier League": "Apr 29, 1961",
            "Europa League": "May 23, 1984",
            "FA Cup": "May 18, 1991 14:",
            "League Cup": "Feb 24, 2008",
            "Super Cup": "",
            "Community Shield": "Aug 10, 1991",
          },
          expanded: false,
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

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,500;0,700;1,400&display=swap");
</style>
