<template>
  <div class="card container">
    <div class="body row">
      <div class="col-lg-3 col-md-3 col-sm-3">
        {{ timer }}
      </div>
      <div class="progress col-lg-3 col-md-3 col-sm-3">
        <div
          class="progress-bar progress-bar-striped bg-success"
          role="progressbar"
          :style="`width: ${progress}%`"
          :aria-valuenow="`${progress}%`"
          aria-valuemin="0"
          aria-valuemax="100"
        >
          <h2 v-if="current < 18000">Working</h2>
          <h2 v-if="current >= 18000">Done</h2>
        </div>
      </div>
      <div class="Timerbuttons col-lg-6 col-md-6 col-sm-6">
        <button
          @click="$emit('start')"
          :class="['btn', 'btn-primary', `btn-${show}`]"
        >
          Start
        </button>
        <button @click="$emit('stop')" class="btn btn-danger">Stop</button>
        <button @click="$emit('clear')" class="btn btn-warning">Clear</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Timer",
  props: ["timer", "state", "current"],
  computed: {
    progress() {
      return this.current / 180;
    },
    show() {
      if (this.current >= 2) {
        return "disabled";
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.card {
  background-color: #DDD;
  margin: 20px;
  .body {
    display: flex;
    justify-content: center;
    align-items: center;
    align-items: center;
    h2 {
      margin: 10px;
      font-size: 15px;
    }
  }
  .Timerbuttons {
    display: inline-block;
    .btn {
      margin: 10px 5px;
      &:disabled {
        opacity: 0.9;
        cursor: not-allowed;
      }
      //   .btn-btn-disabled {
      //   }
    }
  }
}
</style>