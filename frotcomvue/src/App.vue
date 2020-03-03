<template>
  <div id="app">
      <Admin></Admin>
      <div class="vehicle-information">
    <div class="content">

      <div v-for="vehicle in vehicleList" v-bind:key="vehicle.licensePlate">
  
       License Plate: {{ vehicle.licensePlate}}
      </div>

    </div>
      <div class="vehicle-form">
        <VehicleCreate @vehicleEmitter="addVehicleList"></VehicleCreate>
      </div>
  </div>
  </div> 
</template>

<script>
// @ is an alias to /src
  import Admin from '@/components/admin.vue';
  import VehicleCreate from '@/components/vehicle-create';
  

export default {
  data() {
    return {
      vehicleList: [{liscencePlate: '11-xx-02'}],
    }
  },
  components: {
    Admin, 
    VehicleCreate
  },

  props: ['vehicle'],

  methods: {
  addVehicleList(vehicleList) {
    console.log('=============>'+vehicleList)
    this.vehicleList = vehicleList;
  }}

}

</script>
<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Lato:400,400i,700&display=swap');
#app {
  border: solid #D0D2D6;
  background-color: #F5F5F5;
  overflow: hidden;
  height: 95vh;

  .vehicle-information {
    display: flex;
    align-items: stretch;
    .content {
      height: 80vh;
      width: 30vw;
      border-color: #D0D2D6;
      border-style: none solid none none;
    .vehicle-menu {
      display: flex;
      flex-direction: column;
      width: 30vw;
      .vehicle {
        padding-left: 0.5vw;
        font-size: 1.5vw;
        flex-direction: column;
        border-color: #D0D2D6;
        border-style: none none solid none;
      }
    }
  }
    .vehicle-form {
      margin: 1vw 2vw;
      display: flex;
      flex-direction: row;
      width: 60vw;
    }
  }
}

%font-base {
  font-family: 'Lato';
  color: #283645;
}
</style>
