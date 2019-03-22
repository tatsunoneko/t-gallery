<template>
  <div class="main-view">
    <div class="toolbar" v-if="showOverlap">
      <div class="toolbar__icon">
        <div class="toolbar__icon__inner" @click="onLarger"> 
          <img class="toolbar__img" src="../assets/plus.svg"/>
        </div>
      </div>
      <div class="toolbar__icon">
        <div class="toolbar__icon__inner" @click="onSamller">
          <img class="toolbar__img" src="../assets/minus.svg"/>
        </div>
      </div>
    </div>
    <div class="overlap" v-if="showOverlap" @click="zoomOut">
      <div class="overlap__inner" :style="overlapInnerStyle">
        <img class="overlap__img" :src="imgs[curImgIndex]" :style="overlapImgStyle"/>
      </div>
    </div>
    <div class="btn-area" style="margin-right: 5px">
      <t-button btnType="prev" @click="onBackBtnClick"/>
    </div>
    <div class="img-area" style="cursor: zoom-in;" @click="zoomIn">
      <loading-logo :visible="isLoading"/>
      <img class="img-src" :src="imgs[curImgIndex]" v-show="!isLoading" @load="onLoadEnd"/>
    </div>
    <div class="btn-area" style="margin-left: 5px">
      <t-button btnType="next" @click="onNextBtnClick"/>
    </div>
  </div>
</template>

<style lang="scss">
.toolbar {
  width: 50px;
  height: 150px;
  background: cadetblue;
  z-index: 10000;
  position: fixed;
  top: 100%;
  left: 100%;
  transform: translate(-100%, -100%);

  &__icon {
    width: 50px;
    height: 50px;
    position: relative;

    &__inner {
      cursor: pointer;
      width: 50%;
      height: 50%;
      transform: translate(50%, 50%);
    }
  }

  &__img {
    max-height: 100%;
    max-width: 100%;
  }
}
.overlap {
  position: absolute;
  z-index: 9999;
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  cursor: zoom-out;
  &__inner {
    max-width: 200%;
    max-height: 200%;
    z-index: 9999;
  }
  &__img {
    max-width: 200%;
    max-height: 200%;
    z-index: 9999;
  }
}
.main-view {
  padding: 1%;
  height: 70%;
  display: flex;
}
.img-area {
  width: 100%;
  height: 100%;
  position: relative;
}
.img-src {
  max-width: 100%;
  max-height: 100%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.btn-area {
  width: 10%;
}
</style>


<script lang="ts">
import Vue from 'vue';
import { Component, Prop, Watch } from 'vue-property-decorator';
import TButton from './TButton.vue';
import LoadingLogo from './LoadingLogo.vue';

@Component({
  components: {
    TButton,
    LoadingLogo,
  },
})
export default class MainView extends Vue {
  @Prop({ required: true })
  imgs!: string[];

  @Prop()
  curImgIndex!: number;

  scaleNum: number = 1;
  scalePer: number = 100;
  showOverlap: boolean = false;
  isLoading: boolean = true;
  overlapImgStyle = {
    transform: 'scale(1)',
  };
  overlapInnerStyle = {
    height: '100%',
    width: '100%',
  };

  @Watch('curImgIndex')
  onIndexChange() {
    this.isLoading = true;
  }

  @Watch('showOverlap')
  onShowOverlapChanged() {
    if (this.showOverlap) {
      this.overlapImgStyle.transform = 'scale(1)';
      this.overlapInnerStyle = {
        height: '100%',
        width: '100%',
      };
      this.scaleNum = 1;
      this.scalePer = 100;
    }
  }

  onLoadEnd() {
    this.isLoading = false;
  }

  onBackBtnClick() {
    this.$emit('back');
  }

  onNextBtnClick() {
    this.$emit('next');
  }

  zoomIn() {
    this.showOverlap = true;
  }

  zoomOut() {
    this.showOverlap = false;
  }

  onLarger() {
    this.overlapImgStyle.transform = `scale(${this.scaleNum += 0.1})`;
    this.overlapInnerStyle.height = `${this.scalePer += 10}%`;
    this.overlapInnerStyle.width = this.overlapInnerStyle.height;
  }

  onSamller() {
    this.overlapImgStyle.transform = `scale(${this.scaleNum -= 0.1})`;
    this.overlapInnerStyle.height = `${this.scalePer -= 10}%`;
    this.overlapInnerStyle.width = this.overlapInnerStyle.height;
  }
}
</script>
