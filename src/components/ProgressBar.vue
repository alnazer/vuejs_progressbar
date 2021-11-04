<template>
  <div>
    <div class="_progress" :style="{ width: progressBarWidth + '%' }">
      1dddddddddd
    </div>
  </div>
</template>
<script>
export default {
  name: "ProgressBar",
  data() {
    return {
      progressBarWidth: 0,
    };
  },
  props: {
    msg: String,
    progress: Number,
  },
  methods: {
    change(interval) {
      if (this.progressBarWidth == 100) {
        clearInterval(interval);
      } else {
        this.progressBarWidth++;
      }
    },
  },
  watch: {
    progress: function (newNumber, oldNumber) {
      var _this = this;
      var interval = setInterval(function () {
        if (oldNumber > newNumber) {
          _this.progressBarWidth--;
          if (_this.progressBarWidth <= newNumber) {
            clearInterval(interval);
          }
        } else {
          _this.progressBarWidth++;
          if (_this.progressBarWidth >= newNumber) {
            clearInterval(interval);
          }
        }
      }, 10);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
._progress {
  background-color: #42b983;
  width: 0px;
  height: 20px;
}
</style>
