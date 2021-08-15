<template>
  <div class="v-step" v-if="isSticky" id="tooltip">
    <div class="v-step-header">
      <p>{{ steps[index].target }}</p>
    </div>
    <div class="v-step-content">
      <p>{{ steps[index].content }}</p>
    </div>
    <div class="v-step-action">
      <button class="v-step-button" @click="skipTour()">Skip Tour</button>
      <button class="v-step-button" @click="previousTour()" v-if="index > 0">
        Previous
      </button>
      <button class="v-step-button ml-5" @click="nextTour()">Next</button>
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
    };
  },
  mounted() {
    console.log("le", this.length);
    this.createTour();
  },
  methods: {
    skipTour() {
      this.isSticky = !this.isSticky;
    },
    createTour() {
      const tooltip = document.querySelector("#tooltip");
      var targetElement = document.querySelector(
        this.$props.steps[this.index].target
      );
      if (targetElement) {
        createPopper(targetElement, tooltip);
      }
    },
    nextTour() {
      this.index++;
      if (this.index < this.length) {
        this.createTour();
      } else {
        this.skipTour();
      }
    },
    previousTour() {
      this.index--;
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
  margin-top: 0.5rem;
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
</style>
