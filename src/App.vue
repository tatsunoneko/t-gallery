<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <div class="example">
      <t-gallery :imgs="links"/>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import TGallery from './TGallery.vue';

@Component({
  components: {
    TGallery,
  },
})
export default class App extends Vue {
  localPath: string = require('./assets/awdsm.png');
  links: string[] = [];
  created() {
    for (let i = 0; i < 100; i += 1) {
      this.links.push(`https://bing.ioliu.cn/v1?d=${i}&w=1920&h=1080`);
    }
  }
}
</script>

<style>
body {
  margin: 0px;
  height: 100%;
  background: #2c3e50;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.example {
  height: fit-content;
  width: fit-content;
  margin: auto;
}
</style>
