<template>
  <div class="btn" @click="onClick">
    <div :class="['icon', btnName]">
    </div>
  </div>
</template>

<style lang="scss">
.btn {
  height: 100%;
  width: 100%;
  background: whitesmoke;
  &:hover {
    background: #d0d0d0;
  }
}
.icon {
  background: black;
  height: 100%;
  width: 100%;
  -webkit-mask-repeat: no-repeat;
  -webkit-mask-size: 30px;
  -webkit-mask-position-x: center;
  -webkit-mask-position-y: center;
  &:hover {
    background: #6d6d6d;
  }
  &--next {
    -webkit-mask-image: url('../assets/next.svg');
  }
  &--prev {
    -webkit-mask-image: url('../assets/back.svg');
  }
}
</style>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class TButton extends Vue {
  @Prop()
  btnType?: string;

  btnName: string = `icon--${this.btnType}`;

  onClick() {
    this.$emit('click');
  }
}
</script>
