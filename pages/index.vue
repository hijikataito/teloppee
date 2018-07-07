<template lang="pug">
  section.container
    h1.title てろっぴ for VTuber
       
    .columns
      .column
        label.label プレビュー
        svg(xmlns="http://www.w3.org/2000/svg" ref="svg" id="screen" :viewBox="`0 0 ${width} ${height}`" :width="width" :height="height")
          text(:font-size="fontSize" :x="x" :y="y" v-html="messageXml" text-anchor="middle")
      .column
        .field
          label.label テロップ
          textarea.textarea(v-model="message")
      
          label.label フォントサイズ 
          input.input(type="number" v-model.number="fontSize")

          label.label 行の高さ
          input.input(type="number" v-model.number="lineHeight")
          
          label.label 位置X（px）
          input.input(type="number" v-model.number="x")
          
          label.label 位置Y（px）
          input.input(type="number" v-model.number="y")
          
          label.label 画像横サイズ（px）
          input.input(type="number" v-model.number="width")
          
          label.label 画像縦サイズ（px）
          input.input(type="number" v-model.number="height")

        button.button.is-primary.is-large(@click="download") PNGダウンロード
</template>

<script>
// import AppLogo from "~/components/AppLogo.vue";
import { saveSvgAsPng } from "save-svg-as-png";

export default {
  data() {
    return {
      width: 1280,
      height: 720,
      fontSize: 50,
      lineHeight: 60,
      x: 600,
      y: 300,
      message: "Test Telop"
    };
  },
  computed: {
    messageXml() {
      const lines = this.message.split(/\r?\n/);
      let currentX = this.x;
      let currentY = 0;
      let lineHeight = this.lineHeight;
      let html = "";
      lines.forEach(function(line) {
        html += `<tspan x="${currentX}" y="${currentY}">${line}</tspan>`;
        currentY += lineHeight;
      });
      return html;
    }
  },
  methods: {
    download() {
      const name = `${this.message}.png`;
      saveSvgAsPng(document.getElementById("screen"), name);
    }
  },
  components: {}
};
</script>

<style>
#screen {
  border: 1px solid #ccc;
  width: 100%;
  height: auto;
}
</style>
