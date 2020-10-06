<template>
  <div>
    <div class="club border-gray-400 border-solid border-2 p-2">
      <div class="club-summary mb-2 cursor-pointer">
        <p class="text-xl mb-3">
          <img :src="require(`../assets/images/clubs/${logo}`)" :alt="club.name + ' crest'" class="h-10 w-10 mr-4 inline" />{{ club.name }}
        </p>
        <p class="text-base">
          Since Last Trophy: <span class="font-bold"> {{ lastTrophy.length ? lastTrophy[0] : "None Selected!" }} </span>
        </p>
        <p class=" italic">{{ lastTrophy.length ? lastTrophy[1] + ":" : "" }} {{ lastTrophy.length ? lastTrophy[2] : "" }}</p>
      </div>
      <div class="club-detailed">
        <hr class=" mb-2" />
        <div class="since-trophy" v-for="(won, trophy) in filter" :key="trophy">
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
      if (!years) return `${days} days`;
      return `${years} years and ${days} days`;
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
