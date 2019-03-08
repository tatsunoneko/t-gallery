<template>
  <div class="main-view">
    <div class="btn-area">
      <t-button btnType="prev"/>
    </div>
    <div class="img-area">
      <img class="img-src" :src="img"/>
    </div>
    <div class="btn-area">
      <t-button btnType="next"/>
    </div>
  </div>
</template>

<style lang="scss">
.main-view {
  padding: 1%;
  height: 70%;
  display: flex;
}
.img-area {
  width: 100%;
  height: 100%;
}
.img-src {
  max-width: 100%;
  max-height: 100%;
}
.btn-area {
  width: 10%;
}
</style>


<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';
import TButton from './TButton.vue';

@Component({
  components: {
    TButton,
  },
})
export default class MainView extends Vue {
  @Prop({ required: true })
  img!: string;
}
</script>
