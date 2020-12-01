<template>
  <div class="home container h-100">
    <div class="intro h-100">
      <div class="row h-100 justify-content-center align-items-center">
        <div class="col-lg-8 col-md-9 col-sm-12">
          <div class="title">
            <span class="work text-primary">Work</span>
            <span class="timer text-warning">Timer</span>
          </div>
          <Timer
            :timer="timerformate"
            :state="timerstate"
            :current="currentTimer"
            @start="StartTimer"
            @stop="StopTimer"
            @clear="cleartimer"
          />
        </div>
        <div class="col-lg-4 col-md-3 col-sm-12">
          <img src="@/assets/timer.svg" class="img-fluid" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
let strseconds = window.localStorage.getItem("key");
let strformate = window.localStorage.getItem("key2");
import Timer from "@/components/Timer.vue";

export default {
  name: "Home",
  components: {
    Timer,
  },
  data() {
    return {
      timerstate: "stopped",
      currentTimer: strseconds ? JSON.parse(strseconds) : 0,
      timerformate: strformate ? JSON.parse(strformate) : "00:00:00",
      ticker: undefined,
    };
  },
  computed: {
    Congratiolation() {
      if (this.currentTimer == 18000) {
        this.StopTimer();
        alert("COngrationaltion you done your work today!");
      }
    },
  },
  methods: {
    StartTimer() {
      if (this.timerstate !== "running") {
        this.tick();
        this.timerstate = "running";
      }
    },
    tick() {
      this.ticker = setInterval(() => {
        this.currentTimer++;
        this.timerformate = this.formatTime(this.currentTimer);
      }, 1000);
    },
    formatTime(seconds) {
      let measuredtime = new Date(null);
      measuredtime.setSeconds(seconds);
      let MHS = measuredtime.toISOString().substr(11, 8);
      return MHS;
    },
    StopTimer() {
      this.saveData();
      window.clearInterval(this.ticker);
      this.timerstate = "stopped";
    },
    saveData() {
      window.localStorage.setItem("key", JSON.stringify(this.currentTimer));
      window.localStorage.setItem("key2", JSON.stringify(this.timerformate));
    },
    cleartimer() {
      this.currentTimer = 0;
      this.timerformate = "00:00:00";
      window.localStorage.clear();
    },
  },
  destroyed() {
    window.localStorage.clear();
  },
};
</script>
<style lang="scss" scoped>
.home {
  padding-top: 50px;
  .title {
    .work {
      font-size: 40px;
      font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
    }
    .timer {
      font-size: 25px;
    }
  }
}
</style>