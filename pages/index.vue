<template>
  <section class="container">
    <div>
      <h1 class="title">
        teloppee
      </h1>
      <svg xmlns="http://www.w3.org/2000/svg" ref="svg" id="screen" :viewBox="`0 0 ${width} ${height}`" :width="width" :height="height">
        <text font-size="40" :x="x" :y="y">{{ message }}</text>
      </svg>
      <p>
        Text:
        <textarea v-model="message"></textarea>
      </p>
      Width: <input v-model.number="width" />
      <br/> Height: <input v-model="height" />
      <button @click="download">Download</button>
    </div>
  </section>
</template>

<script>
// import AppLogo from "~/components/AppLogo.vue";
import { saveSvgAsPng } from "save-svg-as-png";

export default {
  data() {
    return {
      width: 1280,
      height: 720,
      x: 600,
      y: 300,
      message: "Test Telop"
    };
  },
  methods: {
    download() {
      saveSvgAsPng(document.getElementById("screen"), "diagram.png");
    }
  },
  components: {}
};
</script>

<style>
#screen {
  border: 1px solid #ccc;
  width: 50%;
  height: 50%;
}
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
