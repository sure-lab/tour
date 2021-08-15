<template>
  <div>
    <div class="navbar">
      <a href="#home" id="v-step-0">KOSA</a>
      <div class="dropdown" id="v-step-1">
        <button class="dropbtn">
          Solutions
          <i class="fa fa-caret-down"></i>
        </button>
        <div class="dropdown-content">
          <a href="#">Data Editor</a>
          <a href="#">Model Monitor</a>
        </div>
      </div>
    </div>
    <div class="box">
      <h1>KOSA helps you build more responsible AI.</h1>
      <p>
        Our state-of-the-art technology enables you to understand and mitigate
        AI risks.
      </p>
      <div id="v-step-2">
        <button class="btn default">Get Started</button>
      </div>
    </div>
    <v-tour :steps="steps"></v-tour>
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
          header: {
            title: "Get Started",
          },
          content: `Discover <strong>Vue Tour</strong>!`,
        },
        {
          target: "#v-step-1",
          content: "An awesome plugin made with Vue.js!",
          params: "left",
        },
        {
          target: "#v-step-2",
          content:
            "Try it, you'll love it!<br>You can put HTML in the steps and completely customize the DOM to suit your needs.",
          params: {
            placement: "top",
          },
        },
      ],
    };
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
  text-align: left;
  margin: 0.5rem;
  width: 100px;
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
.dropdown {
  float: right;
  margin-right: 2rem;
  overflow: hidden;
}
.dropdown .dropbtn {
  font-size: 16px;
  border: none;
  outline: none;
  color: black;
  font-weight: 700;
font-weight: bold;
  padding: 14px 16px;
  background-color: inherit;
  font-family: inherit;
  margin: 0;
}

.navbar a:hover,
.dropdown:hover .dropbtn {
  background-color: #04aa6d;
}
.dropdown-content {
  display: none;
  position: absolute;
  background-color: white;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}
.dropdown-content a {
  float: none;
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  text-align: left;
}
.dropdown-content a:hover {
  background-color: #ddd;
}

.dropdown:hover .dropdown-content {
  display: block;
}

.box {
  margin-top: 12rem;
}
.btn {
  border: 2px solid black;
  background-color: white;
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
  background: #e7e7e7;
}
</style>
