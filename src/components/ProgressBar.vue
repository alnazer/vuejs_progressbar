<template>
  <div>
    <div class="progrssbar">
      <div
        class="progrssbar-line"
        v-bind:class="funClassColor()"
        :style="{ width: progressBarWidth + '%' }"
      >
        <div class="progrssbar-percent" v-bind:class="funClassColor()">
          {{ progressBarWidth }}%
        </div>
      </div>
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
    funClassColor() {
      if (this.progressBarWidth >= 80) {
        return "green";
      } else if (this.progressBarWidth >= 50) {
        return "blue";
      } else if (this.progressBarWidth >= 30) {
        return "yellow";
      } else {
        return "red";
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
      this.funClassColor();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.progrssbar {
  background-color: #dee0e9;
  height: 10px;
  margin-top: 5px;
  position: relative;
  width: 100%;
}

.progrssbar-line {
  display: inline-block;
  border-radius: 3px;
  height: 8px;
  right: 0;
  max-width: 100%;
  position: absolute;
}
.green {
  background-color: #0cad4f;
}
.green::after {
  border-color: #0cad4f transparent transparent;
}
.yellow {
  background-color: #ecb05a;
}
.yellow::after {
  border-color: #ecb05a transparent transparent;
}
.blue {
  background-color: #228fec;
  border-color: #228fec transparent transparent;
}
.blue::after {
  border-color: #228fec transparent transparent;
}
.red {
  background-color: rgb(139, 2, 2);
}
.red::after {
  border-color: rgb(139, 2, 2) transparent transparent;
}
.progrssbar-percent {
  border-radius: 3px;
  color: #fff;
  display: inline-block;
  font: 400 12px/12px Open Sans, sans-serif;
  padding: 7px 10px;
  position: absolute;
  left: -23px;
  top: -33px;
}
.progrssbar-percent::after {
  border-style: solid;
  border-width: 4px 3.5px 0 3.5px;

  bottom: -4px;
  content: " ";
  height: 0;
  right: 50%;
  margin-right: -3.5px;
  position: absolute;
  width: 0;
}
</style>
