<template>
<div class="ncard" :style="{'background-color': color}">
  <slot></slot>
</div>
</template>
<script lang='ts'>
import { Component, Vue, Prop } from 'vue-property-decorator';
import randomColor from 'randomcolor';
@Component({

})
export default class Card extends Vue {
  @Prop(String) name: string = String(Math.random());
  color: string = randomColor({ seed: name, luminosity: 'bright' });
}
</script>
<style lang="scss" scoped>
.ncard {
  padding: 10px;

  border-radius: 5px;
  color: inherit;
  text-decoration: inherit;
}
</style>
