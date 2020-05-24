<template>
  <div v-if="loaded">
    <div class="text-3xl text-center">
      {{ dayString }}, {{ month }} {{ dayNumber }}{{ dateSuffix }} {{ year }}
      <div class="label text-xs">
        {{ timezone }}
      </div>
    </div>

    <div class="flex justify-center content-center text-6xl">
      <!-- Hours -->
      <div class="hours relative mr-2">
        {{ hours }}
        <div class="hours label text-sm absolute bottom-0 inset-x-0">hours</div>
      </div>

      <span class="leading-snug">:</span>

      <!-- Minutes -->
      <div class="minutes relative mx-2">
        {{ minutes }}
        <div class="minutes label text-sm absolute bottom-0 inset-x-0">
          minutes
        </div>
      </div>

      <span class="leading-snug">:</span>

      <!-- Seconds -->
      <div class="seconds relative ml-2">
        {{ seconds }}
        <div class="seconds label text-sm absolute bottom-0 inset-x-0">
          seconds
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "Clock",
  data: () => ({
    loaded: false,
    dayString: "Daturday",
    dayNumber: "00",
    month: "Noverder",
    year: "2020",
    hours: "00",
    minutes: "00",
    seconds: "00"
  }),
  mounted() {
    this.updateClock();
    this.monitorTime();
  },
  computed: {
    timezone() {
      const tz = -(new Date().getTimezoneOffset() / 60);
      return `GMT+${tz}`;
    },
    dateSuffix() {
      switch (+this.dayNumber % 10) {
        case 1:
          return "st";
        case 2:
          return "nd";
        case 3:
          return "rd";
        default:
          return "th";
      }
    }
  },
  methods: {
    padTime(num: number): string {
      return num < 10 ? `0${num}` : `${num}`;
    },
    monitorTime() {
      setInterval(() => this.updateClock(), 1000);
    },
    updateClock() {
      const now = new Date();

      const months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ];
      const days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday"
      ];

      this.dayString = days[now.getDay()];
      this.dayNumber = "" + now.getDate();
      this.month = months[now.getMonth()];
      this.year = "" + now.getFullYear();

      this.hours = this.padTime(now.getHours());
      this.minutes = this.padTime(now.getMinutes());
      this.seconds = this.padTime(now.getSeconds());

      this.loaded = true;
    }
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
