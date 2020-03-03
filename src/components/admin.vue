<template>
  <div class="container">
    <div class="header"><h1> {{header}} </h1></div>
    <div class="title"><h2>{{type}}</h2></div>
  </div>
</template>


<script>
import { Component, Vue } from 'vue-property-decorator';
import { VehicleCreate } from './vehicle-create.vue';

@Component
export default class Admin extends Vue {
header = 'ADMININSTRATION';
type = 'VEHICLES';
}
</script>

<style lang="scss">
.container {
    .header {
      text-align: center;

      h1 {
        text-align: center;
        @extend %font-base;
        font-size: 3vw;
      }
    }

    .title {
      border-color: #D0D2D6;
      border-style: solid none;
      h2 {
        text-align: center;
        @extend %font-base;
        font-size: 2vw;
      }
    } 
}
%font-base {
  font-family: 'Lato';
  color: #283645;
}
</style>