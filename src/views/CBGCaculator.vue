<template>
<div id="cbg">
  <p>藏宝阁 <input type="number" v-model="cbgprice" @input="updateFormula()"> 元/万铜币</p>
  <p>寄售元宝 <input type="number" v-model="storeprice" @input="updateFormula()"> 铜币/元宝</p>
  <br>
  <p>
    <input type="number" v-model="yuanbao" @input="updateFormula('yuanbao')" step="1">
    元宝 {{fromYuanbao?'->':'<-'}}
    <input type="number" v-model="coin" @input="updateFormula('coin')" step="10000">
    铜币 {{fromYuanbao?'(寄售有2.5%手续费) ':''}} {{fromCBG?'<-':'->'}}
    <input type="number" v-model="rmb" @input="updateFormula('rmb')" step="0.01">
    元 {{fromCBG?'':`(藏宝阁5%手续费，实收 ${outcome} 元)`}}
    <br>
    溢价率 {{rate}}% {{fromCBG?'(如果你去换绑定元宝的话)':fromYuanbao?'':'(如果你用藏宝阁卖得的钱去买元宝的话)'}}
  </p>
</div>
</template>
<script lang='ts'>
import { Component, Vue, Model } from 'vue-property-decorator';

@Component({})
export default class CBGCaculator extends Vue {
  @Model('input', { type: Number })
  cbgprice: number = 4;
  @Model('input', { type: Number })
  storeprice: number = 350;
  @Model('input', { type: Number })
  yuanbao: number = 100;
  @Model('input', { type: Number })
  coin!: number;
  @Model('input', { type: Number })
  rmb!: number;

  fromYuanbao: boolean = true;
  fromCBG: boolean = false;
  get outcome() {
    let z = this.rmb * 0.95;
    return z.toFixed(2);
  }
  get rate() {
    let z;
    if(this.fromCBG){
      z = ((this.yuanbao / 10)/this.rmb  - 1) * 100;
    }else{
      z = ((this.rmb * 0.95) / (this.yuanbao / 10) - 1) * 100;
    }
    return z.toFixed(2);
  }

  mounted() {
    this.updateFormula();
  }
  updateFormula(base?: string): void {
    switch (base) {
      case 'yuanbao':
        this.coin = this.yuanbao * this.storeprice * 0.975;
        this.rmb = (this.coin / 10000) * this.cbgprice;
        this.fromYuanbao = true;
        this.fromCBG = false;
        break;
      case 'coin':
        this.yuanbao = this.coin / this.storeprice;
        this.rmb = (this.coin / 10000) * this.cbgprice;
        this.fromYuanbao = false;
        this.fromCBG = false;
        break;
      case 'rmb':
        this.coin = (this.rmb / this.cbgprice) * 10000;
        this.yuanbao = this.coin / this.storeprice;
        this.fromYuanbao = false;
        this.fromCBG = true;
        break;
      default:
        if (this.fromYuanbao) {
          this.updateFormula('yuanbao');
        } else if (this.fromCBG) {
          this.updateFormula('rmb');
        } else {
          this.updateFormula('coin');
        }
        break;
    }
  }
}
</script>
<style lang="scss" scoped>
#cbg {
  width: 100%;
  margin: auto;
  text-align: left;
  input {
    width: 70px;
  }
}
</style>
