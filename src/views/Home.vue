<template>
<div class="home">
  <div class="cards-container">
    <Card target='cbg'>
      <h3><router-link :to="{name: 'cbg'}" name='cbg'>藏宝阁元宝计算器</router-link></h3>
    </Card>
  </div>
</div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Card from '@/components/widgets/Card.vue';

@Component({
  components: {
    Card,
  },
})
export default class Home extends Vue {}
</script>

<style lang="scss">
.home {
  display: flex;
  flex: 1 1 auto;
  align-items: center;
  justify-content: center;
  .cards-container {
    padding: 0 100px;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }
  a {
    color: inherit;
    text-decoration: inherit;
  }
}
</style>