<template>
    <div id="main-grid" class="crop" v-bind:style=" print ? 'background-color: white;' : 'background-color: #BA7331;' "> 
      <h3 id="crop-name" v-bind:style=" print ? 'color: black;' : 'color: white;' ">{{crop.name}}</h3>
      <h3 id="crop-amount" v-bind:style=" print ? 'color: black;' : 'color: white;' ">{{crop.amount * crop.cropsPerSqFt}} {{plantsss}}</h3>
      <h3 id="cost" v-bind:style=" print ? 'color: black;' : 'color: white;' ">${{(crop.seed_cost * (crop.amount * crop.cropsPerSqFt)).toFixed(2)}}</h3>
  </div>
</template>

<script>

export default {
    name: 'print',
    props: {
        crop: Object
    },
    data() {
      return {
          print: false,
      };
    },
    created() {
      if(this.$route.name == 'print') {
          this.print = true;
      }
    },
    computed: {
        plantsss() {
            if(this.crop.amount * this.crop.cropsPerSqFt > 1) {
                return 'plants'
            } else {
                return 'plant'
            }
        }
    }
}
</script>

<style scoped>

#main-grid{
  display: grid;
  grid-auto-flow:row;
  grid-template-columns:1fr 1fr 1fr;
  grid-template-areas:
    "crop-name crop-amount cost";
  padding: 0px;
  color: white;
  background-color: #BA7331;
  margin-left: 10px;
  margin-right: 10px;
  border-radius: 0px;
}
#crop-name{
  grid-area: crop-name;
  color:white;
  font-size: 20px;
  padding-top: 7px;
  padding-left: 25px;
  text-align:center;
  
}
#crop-amount{
  grid-area: crop-amount;
  background: none;
  color:white;
  font-size: 20px;
  padding-top: 7px;
  padding-left: 25px;
  text-align: center;

}
#cost{
  grid-area: cost;
  background: none;
  color:white;
  font-size: 20px;
  padding-top: 7px;
  padding-left: 25px;
  text-align: center;
}
@media (max-width: 400px){

#crop-name{
  font-size: 12px;
}
#crop-amount{
  font-size: 12px;
}
#cost{
  font-size: 12px;
}
}

</style>