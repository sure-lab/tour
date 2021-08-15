<template>
  <div class="v-step" v-if="isSticky" id="tooltip">
    <div class="v-step-header" v-if="steps[index].header">
      <p>{{ steps[index].header }}</p>
    </div>
    <div class="v-step-content" v-if="steps[index].content">
      <p>{{ steps[index].content }}</p>
    </div>
    <div class="v-step-action">
      <button class="v-step-button" @click="skipTour()">Skip Tour</button>
      <button class="v-step-button" @click="previousTour()" v-if="index > 0">
        Previous
      </button>
      <button class="v-step-button ml-5" @click="nextTour()">
        {{ index + 1 == length ? "Finish" : "Next" }}
      </button>
    </div>
  </div>
</template>
<script>
import { createPopper } from "@popperjs/core";

export default {
  props: {
    steps: [],
  },
  data() {
    return {
      isSticky: true,
      index: 0,
      length: this.$props.steps.length,
      next: false,
      pre: false,
    };
  },
  mounted() {
    this.createTour();
  },
  methods: {
    skipTour() {
      //  var targetElement = document.querySelector(
      //   this.$props.steps[this.index].target
      // );
      this.isSticky = !this.isSticky;
      this.$emit("toggleOverlay");
    },
    createTour() {
      const tooltip = document.querySelector("#tooltip");
      var targetElement = document.querySelector(
        this.$props.steps[this.index].target
      );
      if (this.index === 0 && !this.pre) {
        this.$emit("targetElement", { ele: targetElement });
      } else if (this.index != 0 && this.next) {
        var targetElement2 = document.querySelector(
          this.$props.steps[this.index - 1].target
        );
        this.$emit("targetElement", {
          ele: targetElement,
          elePre: targetElement2,
        });
      } else if (this.index != 0 && this.pre) {
        var targetElement3 = document.querySelector(
          this.$props.steps[this.index + 1].target
        );
        this.$emit("targetElement", {
          ele: targetElement,
          elePre: targetElement3,
        });
      } else {
        var targetElement4 = document.querySelector(
          this.$props.steps[this.index + 1].target
        );
        this.$emit("targetElement", {
          ele: targetElement,
          elePre: targetElement4,
        });
      }

      if (targetElement) {
        createPopper(
          targetElement,
          tooltip,
          this.$props.steps[this.index].params
        );
      }
    },
    nextTour() {
      this.index++;
      this.next = true;
      if (this.index < this.length) {
        this.createTour();
      } else {
        this.skipTour();
      }
    },
    previousTour() {
      this.index--;
      this.next = false;
      this.pre = true;
      this.createTour();
    },
  },
};
</script>
<style lang="css" scoped>
.v-step {
  background: #50596c;
  color: #fff;
  max-width: 350px;
  border-radius: 3px;
  -webkit-box-shadow: transparent 0 0 0 0, transparent 0 0 0 0,
    rgb(0 0 0 / 10%) 0 4px 6px -1px, rgb(0 0 0 / 6%) 0 2px 4px -1px;
  box-shadow: 0 0 0 0 transparent, 0 0 0 0 transparent,
    0 4px 6px -1px rgb(0 0 0 / 10%), 0 2px 4px -1px rgb(0 0 0 / 6%);
  padding: 1rem;
  pointer-events: auto;
  text-align: center;
  z-index: 10000;
}
.v-step-header {
  text-align: center;
}
.v-step-content {
  text-align: center;
  margin: 0.8rem;
}
.v-step-action {
  text-align: center;
  margin: 0 0 1rem 0;
}
.v-step-button {
  background: transparent;
  border: 0.05rem solid #fff;
  border-radius: 0.1rem;
  color: #fff;
  cursor: pointer;
  display: inline-block;
  font-size: 0.8rem;
  height: 1.8rem;
  line-height: 1rem;
  outline: none;
  margin: 0 0.8rem;
  padding: 0.35rem 0.6rem;
  text-align: center;
  text-decoration: none;
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
  vertical-align: middle;
  white-space: nowrap;
}
.step-overlay {
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.visible {
  position: relative;
  z-index: 1;
}
</style>
