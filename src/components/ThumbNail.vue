<template>
  <div :class="['thumb-nail', selected ? 'thumb-nail--selected' : '']" @click="onClick">
    <div class="img-area">
      <loading-logo :visible="isLoading"/>
      <img class="img-src" :src="img" v-show="!isLoading" @load="onLoadEnd" @error="onError"/>
    </div>
  </div>
</template>

<style lang="scss">
.thumb-nail {
  height: 95%;
  max-width: 140px;
  width: 140px;
  border-width: 2px;
  border-color: #6d6d6d;
  border-style: solid;
  margin-left: 2px;
  margin-right: 2px;

  &:hover {
    border-color: blue;
  }

  &--selected {
    border-color: blueviolet;
  }
}
</style>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';
import LoadingLogo from './LoadingLogo.vue';

@Component({
  components: {
    LoadingLogo,
  },
})
export default class ThumbNail extends Vue {
  @Prop()
  img?: string;

  @Prop()
  selected?: boolean;

  isLoading: boolean = true;

  onLoadEnd(event: Event) {
    this.isLoading = false;
  }

  onError() {
    this.$emit('loadingError');
  }

  onClick() {
    this.$emit('click');
  }
}
</script>
