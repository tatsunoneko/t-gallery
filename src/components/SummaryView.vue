<template>
  <div class="summary-view">
    <div class="summary-view-inner" :style="innerStyle">
      <thumb-nail 
        v-for="el in srcAry"
        :key="el.key"
        :img="el.path"
        :selected="el.key === curKey"
        @click="onClick(el.key, el.path)"
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

  innerStyle = {
    width: '0px',
  };

  mounted() {
    const totalWidthNum = this.imgs.length * 144;
    this.innerStyle = {
      width: `${totalWidthNum}px`,
    };
    for (let i = 0; i < this.imgs.length; i += 1) {
      this.srcAry.push({
        key: i,
        path: this.imgs[i],
      });
    }
  }

  onClick(key: number) {
    this.$emit('imageChange', key);
  }
}
</script>
