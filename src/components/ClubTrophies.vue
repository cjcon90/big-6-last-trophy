<template>
  <div class="w-full mx-auto sm:max-w-xl">
    <div
      class="club p-4 leading-7"
      :style="{
        backgroundColor: club.colorPrimary,
        color: club.colorSecondary,
      }"
    >
      <!-- <img src="../assets/images/down-chevron.svg" alt="expand icon" class="h-8 absolute bottom-0 right-0 fill-current" /> -->
      <div class="club-summary mb-2 cursor-pointer relative" @click="club.expanded = !club.expanded">
        <i :class="club.expanded ? 'fas fa-chevron-up' : 'fas fa-chevron-down'" class=" absolute right-0 bottom-0"></i>
        <!-- <svg
          id="Capa_1"
          enable-background="new 0 0 551.13 551.13"
          viewBox="0 0 551.13 551.13"
          width="25"
          xmlns="http://www.w3.org/2000/svg"
          class="absolute fill-current bottom-0 right-0 divide-opacity-75"
        >
          <path d="m275.565 361.679-223.897-223.896h-51.668l275.565 275.565 275.565-275.565h-51.668z" />
        </svg> -->
        <p class="text-3xl mb-3 font-serif">
          <img :src="require(`../assets/images/clubs/${logo}`)" :alt="club.name + ' crest'" class="h-10 w-10 mr-4 inline" />{{ club.name }}
        </p>
        <p class=" text-lg">
          Since Last Trophy:
          <span class="font-bold">
            {{ lastTrophy.length ? lastTrophy[0] : "None Selected!" }}
          </span>
        </p>
        <p class=" italic">
          {{ lastTrophy.length ? lastTrophy[1] + ":" : "" }}
          {{ lastTrophy.length ? lastTrophy[2] : "" }}
        </p>
      </div>
      <div class=" h-px w-11/12 mx-auto my-4 opacity-75" :style="{ backgroundColor: club.colorSecondary }" v-if="club.expanded"></div>
      <div class="club-detailed" v-show="club.expanded">
        <div class="since-trophy text-lg" v-for="(won, trophy) in filter" :key="trophy">
          <p v-if="won">{{ trophy }}: {{ formatTime(timeSince(club.trophies[trophy])) }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ClubTrophies",
  methods: {
    timeSince(time) {
      // if competition never won, return N/A
      if (!time) return;
      //get date trophy was won
      let trophyWon = new Date(time).getTime();
      //get today's date
      let now = new Date().getTime();
      // Find the distance between now and the count down date
      return now - trophyWon;
    },
    formatTime(time) {
      if (!time) return "N/A";
      // Time calculations for days, hours, minutes and seconds
      let years = Math.floor(time / 31536000000);
      let days = Math.floor((time - years * 31536000000) / (1000 * 60 * 60 * 24));

      // Output the result
      if (!years) {
        return `${days} days`;
      } else if (years === 1) {
        return `${years} year, ${days} days`;
      }
      return `${years} years, ${days} days`;
    },
  },
  computed: {
    lastTrophy() {
      let arr = [];
      for (let [trophy, won] of Object.entries(this.filter)) {
        if (won) arr.push([this.timeSince(this.club.trophies[trophy]), trophy, won]);
      }
      if (!arr.length) return "";
      let time;
      arr.map((trophyWin) => {
        if (!time || !time[0]) time = trophyWin;
        else if (trophyWin[0] < time[0]) time = trophyWin;
      });
      return [this.formatTime(time[0]), time[1], this.club.trophies[time[1]]];
    },
  },
  props: {
    club: Object,
    logo: String,
    filter: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
