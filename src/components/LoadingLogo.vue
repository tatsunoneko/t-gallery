<style lang="scss">
.loading {
  &-container {
    width: 100%;
    height: 100%;
  }

  &-logo {
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    position: absolute;
  }
}
</style>

<script lang="tsx">
import Vue, { VNode, CreateElement } from 'vue';
import { Component, Prop } from 'vue-property-decorator';

@Component
export default class LoadingLogo extends Vue {
  @Prop()
  visible!: boolean;

  defaultSvgPath = require('../assets/loading.svg');

  render(h: CreateElement): VNode {
    return (
      <transition name='fade'>
        { this.visible ?
        <div class='loading-container'>
          <img class='loading-logo' src={this.defaultSvgPath}/>
        </div> : null }
      </transition>
    ) as VNode;
  }
}
</script>
