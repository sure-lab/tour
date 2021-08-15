<template>
  <div id="overlay">
    <div class="navbar">
      <a href="#home" id="v-step-0"> KOSA</a>
      <div id="v-step-1" class="title">Solutions</div>
    </div>
    <div class="box">
      <h1>KOSA helps you build more responsible AI.</h1>
      <p>
        Our state-of-the-art technology enables you to understand and mitigate
        AI risks.
      </p>
      <div>
        <button class="btn default" id="v-step-2">Get Started</button>
      </div>
    </div>
    <v-tour
      :steps="steps"
      @toggleOverlay="closeOverlay($event)"
      @targetElement="createOverlay($event)"
    ></v-tour>
  </div>
</template>

<script>
import VTour from "./layout/VTour.vue";
export default {
  name: "WelcomePage",
  components: {
    VTour,
  },
  data() {
    return {
      steps: [
        {
          target: "#v-step-0",
          header: "Let's Start",
          content: `KOSA helps you build more responsible AI`,
        },
        {
          target: "#v-step-1",
          content: "Solutions we Provide",
          // params: {
          //   placement: "left",
          // },
        },
        {
          target: "#v-step-2",
          content: "Join Us",
        },
      ],
    };
  },
  mounted() {
    this.createOverlay();
  },
  methods: {
    createOverlay(item) {
      if (item) {
        var element = document.getElementById("overlay");
        element.classList.add("step-overlay");
        item.ele.classList.add("visible");
        if (item.elePre) {
          item.elePre.classList.remove("visible");
        }
      }
    },
    closeOverlay(item) {
      var element = document.getElementById("overlay");
      element.classList.remove("step-overlay");
      if(item){
        item.classList.remove("visible");
      }
    },
  },
};
</script>
<style scoped>
h3 {
  margin: 40px 0 0;
}
a {
  color: #42b983;
}
.title {
  margin-top: 0.35rem;
  font-weight: 900;
  font-weight: bold;
  float: right;
  padding: 14px 16px;
  margin-right: 2rem;
  padding: 14px 16px;
  overflow: hidden;
}
.navbar {
  overflow: hidden;
  font-family: Arial;
}

.navbar a {
  float: left;
  font-size: 16px;
  text-align: center;
  font-weight: 900;
  font-weight: bold;
  color: black;
  padding: 14px 16px;
  text-decoration: none;
}

.box {
  margin-top: 12rem;
}
.btn {
  border: 2px solid black;
  background-color: transparent;
  color: black;
  padding: 14px 28px;
  font-size: 16px;
  cursor: pointer;
}
.default {
  border-color: #e7e7e7;
  color: black;
}

.default:hover {
  background: green;
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
  background-color: white;
}
</style>
