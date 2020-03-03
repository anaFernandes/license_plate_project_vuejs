<template>
    <div>
        <div class="content-vehicle">
            <form class="form" method="addList">
                <div class="form-group">
                    <label for="licensePlate" class="control-label">License Plate: </label>
                    <input type="text" class="form-control" required pattern="^([0-9]{2}-[A-Za-z]{2}-[0-9]{2})?$" name="licensePlate" id="licensePlate" placeholder="99-XX-99" v-model="vehicle.licensePlate">
                </div>
                <div class="form-group">
                    <label for="class" class="control-label">Class: </label>
                    <input type="text" class="form-control" name="class" id="class" placeholder="Class" v-model="vehicle.class">
                </div>
                <div class="form-group">
                    <label for="fuelType" class="control-label">Fuel Type: </label>
                    <input type="text" class="form-control" name="fuelType" id="fuelType" placeholder="Fuel Type" v-model="vehicle.fuelType">
                </div>
                <div class="form-group">
                    <label for="odometer" class="control-label">Odometer: </label>
                    <input type="text" class="form-control" name="odometer" id="odometer" placeholder="Odometer" v-model="vehicle.odometer">
                </div>
                <div class="add">
                    <button @click.prevent="addVehicle" class="add-btn">Add</button>
                </div>
            </form>
        </div>
        <div class="submit">
            <button type="submit" class="submit-btn" @click="submit()">Submit</button>
        </div>
    </div>

</template>
<script>
    import { Component, Vue } from 'vue-property-decorator';
    import { monthConst } from '@/assets/monthConst'
    @Component
    export default class VehicleCreate extends Vue {
      listVehicle = [];
      vehicle = {};


    addVehicle() {
      const regex = new RegExp('^([0-9]{2}-[A-Za-z]{2}-[0-9]{2})?$');
      if(this.vehicle.licensePlate && regex.test(this.vehicle.licensePlate)) {
        if(this.listVehicle.length === 0) {
            this.addList();
        } else {
          if(!this.listVehicle.find( el =>  el.licensePlate === this.vehicle.licensePlate)) {
              this.addList();
          }
        }
        this.vehicle = {};
      }
    }

  addList() {
    this.vehicle.manufacture = 'vw';
    this.vehicle.lastDrive = [{driveId: '1234', driverName:'John Doe'}];
    this.listVehicle.push(this.vehicle);
    this.setVisibility('visible');
    console.log(this.listVehicle);
  }

    submit(){
      const currentDate = Date().split(' ');
      const currentMonth = monthConst.indexOf(currentDate[1]);
      const currentHours = currentDate[4].split(':');

      if(sessionStorage.getItem('date')) {
        const date = sessionStorage.getItem('date').split(' ');
        const month = monthConst.indexOf(date[1]);
        const hours = currentDate[4].split(':');

        ///If the current year, month or day is greater than the year, month or from 2 days
        if(currentDate[3] > date[3] || currentMonth > month || parseInt(currentDate[2]) > parseInt(date[2]) + 2 ) {
          this.addSessionStore();

        //If the current month and year is equal of the month in sessionStorage
        } if(currentDate[3] === date[3] && currentMonth === month) {
            // and the current day also the same
            if(currentDate[2] === date[2]  && parseInt(currentHours[0]) >= parseInt(hours[0]) + 2) {
              this.addSessionStore();
            }
            if(parseInt(currentDate[3]) === parseInt(date[3]) + 1 && parseInt(currentHours[0]) >= parseInt(hours[0]) + 24){
              this.addSessionStore();
            }
      } } else {
        this.addSessionStore();
      }
      this.vehicleEmite();
      this.setVisibility('hidden');
    }

    addSessionStore() {
      const date = Date();
      sessionStorage.setItem('vehicleList',JSON.stringify(this.listVehicle));
      sessionStorage.setItem('date', JSON.stringify(date));
    }


    setVisibility(hide) {
      const btnVisibility = document.getElementsByClassName('submit-btn');
      btnVisibility[0].style.visibility = hide;
    }


    vehicleEmite() {
      this.$emit('vehicleEmitter', this.listVehicle);
      this.listVehicle = [];
    }
  }
</script>

<style lang="scss" scoped>
.content-vehicle {
  display: flex;
  border: solid #D0D2D6;

  .form {
    .control-label{
      padding: 0.5vw;
      display: inline-block;
      width: 13vw;
      @extend %font-base;
      font-size: 1.5vw;
    }

    input {
      border: none;
      background-color: #FAFAFA;
      font-size: 1.5vw;
      width: 45vw;
    }
    .add-btn{
      background-color: #65b312;
      margin-bottom: 1vw;
     }
  }
}

.submit {
  .submit-btn {
    float: right;
    background-color: #0074b3;
    margin: 1vw;
    visibility: hidden;
  }
}



P {
  @extend %font-base;
  font-size: 1.2vw;
}


button {
  font-family: 'Lato';
  color: #FAFAFA;
  border-radius: 0.5vw;
  border: none;
  color: white;
  padding: 0.2vh 1vw;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 2vw;
  margin: 0.3vw 1vw;
  cursor: pointer;
}

%font-base {
  font-family: 'Lato';
  color: #283645;
}

</style>