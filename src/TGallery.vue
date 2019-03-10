<template>
  <div class="t-gallery" :style="mainStyle">
    <main-view 
      :imgs="paths" 
      :curImgIndex="curPathIndex"
      @next="onNext"
      @back="onBack"
    />
    <summary-view 
      :imgs="paths" 
      :curKey="curPathIndex"
      @imageChange="imageChange"
    />
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

  mainWidth: string = '550px';
  mainHeight: string = '400px';
  mainStyle = {
    width: this.mainWidth,
    height: this.mainHeight,
  };

  paths: string[] = [];
  curPathIndex: number = 0;

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
    for (const el of this.imgs) {
      this.paths.push(el);
    }
    this.curPathIndex = 0;
  }

  imageChange(pathIndex: number) {
    this.curPathIndex = pathIndex;
  }

  onNext() {
    if (this.curPathIndex + 1 > this.paths.length - 1) {
      this.curPathIndex = 0;
    } else {
      this.curPathIndex += 1;
    }
  }

  onBack() {
    if (this.curPathIndex - 1 < 0) {
      this.curPathIndex = this.paths.length - 1;
    } else {
      this.curPathIndex -= 1;
    }
  }
}
</script>

<style scoped>

</style>
