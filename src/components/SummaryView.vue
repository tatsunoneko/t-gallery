<template>
  <div class="summary-view">
    <div class="summary-view-inner">
      <thumb-nail v-for="el in srcAry" :key="el.key"/>
    </div>
  </div>
</template>

<style lang="scss">
.summary-view {
  height: 26%;
  &-inner {
    margin: 2px;
    display: flex;
    height: 100%;
  }
}
</style>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';
import ThumbNail from './ThumbNail.vue';

@Component({
  components: {
    ThumbNail,
  },
})
export default class SummaryView extends Vue {
  srcAry = [{
    key: '1',
  }, {
    key: '2',
  }, {
    key: '3',
  }, {
    key: '4',
  }, {
    key: '5',
  }];
}
</script>
