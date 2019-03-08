<template>
  <div class="t-gallery" :style="mainStyle">
    <main-view :img="path"/>
    <summary-view/>
  </div>
</template>

<style lang="scss">
.t-gallery {
  border-style: solid;
  border-width: 1px;
  border-color: #333333;
}
</style>


<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import MainView from './components/MainView.vue';
import SummaryView from './components/SummaryView.vue';
@Component({
  components: {
    MainView,
    SummaryView,
  },
})
export default class TGallery extends Vue {
  @Prop({required: true})
  imgs!: string[];

  @Prop()
  width?: string | number;

  @Prop()
  height?: string | number;

  mainWidth: string = '500px';
  mainHeight: string = '400px';
  mainStyle = {
    width: this.mainWidth,
    height: this.mainHeight,
  };

  path: string = require('./assets/1556688458.png');

  created() {
    if (this.width) {
      if (typeof(this.width) === 'string') {
        this.mainWidth = this.width;
      } else {
        this.mainWidth = `${this.width}px`;
      }
    }
    if (this.height) {
      if (typeof(this.height) === 'string') {
        this.mainHeight = this.height;
      } else {
        this.mainHeight = `${this.height}px`;
      }
    }
  }
}
</script>

<style scoped>

</style>
