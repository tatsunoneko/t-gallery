<template>
  <div class="summary-view">
    <div class="summary-view-inner" :style="innerStyle">
      <thumb-nail 
        v-for="el in displayAry"
        :key="el.key"
        :img="el.path"
        :selected="el.key === curKey"
        @click="onClick(el.key, el.path)"
        @loadingError="onLoadingError(el.key)"
      />
    </div>
  </div>
</template>

<style lang="scss">
.summary-view {
  height: 28%;
  overflow: auto;
  &-inner {
    margin: 2px;
    display: flex;
    height: 90%;
  }
}
</style>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';
import ThumbNail from './ThumbNail.vue';
import _ from 'lodash';

export interface Src {
  key: number;
  path: string;
}

@Component({
  components: {
    ThumbNail,
  },
})
export default class SummaryView extends Vue {
  @Prop()
  imgs!: string[];

  @Prop()
  curKey!: number;

  srcAry: Src[] = [];
  startKey: number = 0;
  endKey: number = 0;
  displayAry: Src[] = [];

  innerStyle = {
    width: '0px',
  };

  mounted() {
    let totalWidthNum = 0;
    if (this.imgs.length <= 10) {
      totalWidthNum = this.imgs.length * 144;
      this.endKey = this.imgs.length;
    } else {
      totalWidthNum = 10 * 144;
      this.endKey = 9;
    }
    this.innerStyle = {
      width: `${totalWidthNum}px`,
    };
    for (let i = 0; i < this.imgs.length; i += 1) {
      this.srcAry.push({
        key: i,
        path: this.imgs[i],
      });
    }
    this.displayAry = _.cloneDeep(this.srcAry).slice(this.startKey, this.endKey + 1);
  }

  onLoadingError(index: number) {
    let newPath = this.srcAry[index].path;
    if (newPath.search('/?/') === -1) {
      newPath += `?timestamp=${Date.now()}`;
    } else {
      newPath += `&timestamp=${Date.now()}`;
    }
    this.displayAry[index].path = newPath;
  }

  onClick(key: number) {
    this.$emit('imageChange', key);
  }
}
</script>
