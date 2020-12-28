<template>
  <div class="flex col-auto q-my-sm">
<!--         
        <p>Data actual: {{ strDataActual }} <br>
        <p>Data naixam: {{ strFechaNac }} <br>
        <p>Data aniversari: {{ strFechaCumple }}</p>
 -->



        <div class="row clDiv col-12" >
          <div class="q-pa-sm">
             {{ objAniversari.nom }}  <br>  <span class="clNaix">Data Naix.: {{ strFechaNac }}</span>
          </div>
<!-- 
          <div class="clDiv">
             Data Naix.: {{ strData }} <br/>
             Data actual: {{ dataActual }}
          </div>
 -->
          <div class="column clTemps"> 

            <div class="row inline no-wrap justify-between items-center"> 
              <div class="q-pa-sm text-weight-bold">Temps viscut: </div>
              <div class="row inline q-pa-sm ">
                 <span class="tvNumeros">{{ tvanys }}</span> &nbsp; anys, &nbsp;
                 <span class="tvNumeros">{{ tvmesos }} </span> &nbsp; mesos, &nbsp;
                 <span class="tvNumeros">{{ tvdies }} </span> &nbsp; dies, &nbsp;
                 <span class="tvNumeros">{{ tvhores }} </span> &nbsp; hores, &nbsp;
                 <span class="tvNumeros">{{ tvminuts }} </span> &nbsp; minuts, &nbsp;
                 <span class="tvNumeros">{{ tvsegons }} </span> &nbsp; segons
              </div>
            </div>
            <div class="row inline no-wrap items-center"> 
              <div class="q-pa-sm text-weight-bold">Temps fins dia aniversari: </div>
              <div v-if="dataActualCumple < fechaCumple" class="row inline q-pa-sm ">
                 <span class="tfaNumeros">{{ tfamesos }} </span> &nbsp; mesos, &nbsp;
                 <span class="tfaNumeros">{{ tfadies }} </span> &nbsp; dies, &nbsp;
                 <span class="tfaNumeros">{{ tfahores }} </span> &nbsp; hores, &nbsp;
                 <span class="tfaNumeros">{{ tfaminuts }} </span> &nbsp; minuts, &nbsp;
                 <span class="tfaNumeros">{{ tfasegons }} </span> &nbsp; segons
              </div>
              <div v-else-if="strDataActualCumple === strFechaCumple">
                Avui es el teu cumple: <span class="tfaNumeros q-pa-sm">{{ tvanys }} anys</span> MOLTES FELICITATS !!!
              </div>
              <div v-else>
                Aquest any ja has fet <span class="tfaNumeros q-pa-sm">{{ tvanys }}</span> anys.
              </div>
            </div>

          </div>
<!--           
          <div class="clDiv">
             <q-btn label="arrancar" no-caps @click="arrancar"/>
             <q-btn label="stop" no-caps @click="aturar"/>
          </div>
 -->      
        </div>

  </div>

</template>

<script>
import datetimeDifference from "datetime-difference";

export default {
  // name: 'ComponentName',
  props: [
  	'objAniversari'
  ],

  created () {
    console.log("estic a CREATE");
    //this.fechaNac = new Date(this.objAniversari.dataNaix);
    this.fechaNac = this.objAniversari.dataNaix;
    //console.log("fechaNac: " + this.fechaNac);

    this.dataActual = new Date();

    //var diaActual = this.calcTime('Madrit', 2, new Date());
    //console.log("diaActual: " + diaActual);

    //var strDataActual = diaActual.getFullYear() + "-" + (this.fechaNac.getMonth()+1) + "-" + this.fechaNac.getDate();
    //console.log('strDataActual: ' + strDataActual) ;
    this.fechaCumple = new Date(
                                new Date().getFullYear(),
                                this.fechaNac.getMonth(),
                                this.fechaNac.getDate()
                              );
    //console.log("DataAniversari: " + dataAniversari);
    //this.fechaCumple = dataAniversari;

    this.arrancar();

  },

  data () {
    return {
      tvanys: null,
      tvmesos: null,
      tvdies: null,
      tvhores: null,
      tvminuts: null,
      tvsegons: null,

      //tfaanys: null,
      tfamesos: null,
      tfadies: null,
      tfahores: null,
      tfaminuts: null,
      tfasegons: null,

      fechaNac: null,
      fechaCumple: null,
      dataActual: null,
      dataActualCumple: null,
      pull: null
    }
  },

  methods: {
    aturar: function () {
      clearInterval(this.pull)
      console.log ("pull aturat")
    },

    arrancar: function(){
      var self = this; 

      this.pull = setInterval(function(){
          //self.dataActual = new Date();
          self.dataActual = new Date();
          self.dataActualCumple = new Date(
                                      self.dataActual.getFullYear(),
                                      self.dataActual.getMonth(),
                                      self.dataActual.getDate()
                                      );
          //console.log("fechaCumple: " + self.fechaCumple);
          //console.log("dataActualCumple: " + self.dataActualCumple);

          var resultTempsVida = datetimeDifference(self.fechaNac, self.dataActual);
          self.tvanys = resultTempsVida.years;
          self.tvmesos = resultTempsVida.months;
          self.tvdies = resultTempsVida.days;
          self.tvhores = resultTempsVida.hours;
          self.tvminuts = resultTempsVida.minutes;
          self.tvsegons = resultTempsVida.seconds;

          var resultTempsFinsAniversari = datetimeDifference(self.dataActual, self.fechaCumple);
          //self.anys = resultTempsFinsAniversari.years;
          self.tfamesos = resultTempsFinsAniversari.months;
          self.tfadies = resultTempsFinsAniversari.days;
          self.tfahores = resultTempsFinsAniversari.hours;
          self.tfaminuts = resultTempsFinsAniversari.minutes;
          self.tfasegons = resultTempsFinsAniversari.seconds;

      },1000)

    },

    calcTime: function (city, offset, d) {
        // create Date object for current location
        //var d = new Date();

        // convert to msec
        // subtract local time zone offset
        // get UTC time in msec
        var utc = d.getTime() + (d.getTimezoneOffset() * 60000);

        // create new Date object for different city
        // using supplied offset
        var nd = new Date(utc + (3600000*offset));

        // return time as a string
        //return "The local time for city"+ city +" is "+ nd.toLocaleString();

        return nd;
    }


  },

  computed: {
    strFechaNac: function(){ 
      //console.log("Data Naixam.: " + this.fechaNac.getDate() + "/" + (this.fechaNac.getMonth() + 1) + "/" + this.fechaNac.getFullYear());
      var strFN = this.fechaNac.getDate() + "/" + (this.fechaNac.getMonth() + 1) + "/" + this.fechaNac.getFullYear();
      return strFN;
    },
    strDataActual: function(){ return this.dataActual.toLocaleString() || null },
    strDataActualCumple: function(){ return this.dataActualCumple.toLocaleString() || null },
    strFechaCumple: function(){ return this.fechaCumple.toLocaleString() },

  },


  beforeDestroy () {
    clearInterval(this.pull)
  }

}
</script>

<style>
  .clDiv {
    border: 1px solid blue;
  }

  .tvNumeros{
    font-weight: bold;
    color: blue;
  }
  .tfaNumeros{
    font-weight: bold;
    color: red;
  }
  .clNaix{
    font-size: 10px;
    font-family: courier verdana;
  }

  .clTemps{
    font-size: 12px;
    font-family: verdana;
    border-left: 1px solid blue;
  }
</style>
