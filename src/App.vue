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
  links: string[] = [
    'https://www.bing.com/th?id=OHR.GrapeHarvest_EN-US9833740254_1920x1080.jpg&rf=NorthMale_1920x1080.jpg&pid=hp',
    'https://www.bing.com/th?id=OHR.Policewomen_EN-CN1248152433_1920x1080.jpg&rf=NorthMale_1920x1080.jpg&pid=hp',
    'https://www.bing.com/th?id=OHR.BrittlebushBloom_EN-CN2839869448_1920x1080.jpg&rf=NorthMale_1920x1080.jpg&pid=hp',
    'https://www.bing.com/th?id=OHR.Cefalu_EN-CN2165487733_1920x1080.jpg&rf=NorthMale_1920x1080.jpg&pid=hp',
    'https://www.bing.com/th?id=OHR.MardiGrasIndians_EN-CN1798848109_1920x1080.jpg&rf=NorthMale_1920x1080.jpg&pid=hp',
  ];
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
