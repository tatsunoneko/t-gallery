<template>
  <div class="thumb-nail">
  </div>
</template>

<style lang="scss">
.thumb-nail {
  height: 95%;
  width: 20%;
  border-width: 2px;
  border-color: #6d6d6d;
  border-style: solid;
  margin-left: 2px;
  margin-right: 2px;
}
</style>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';

@Component
export default class ThumbNail extends Vue {

}
</script>
