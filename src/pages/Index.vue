<template>
  <q-page class="flex justify-center content-start">
    <!-- <img alt="Quasar logo" src="~assets/quasar-logo-full.svg"> -->
    <div v-for="(aniversari, index) in aniversaris">
      <cmp_Temps :objAniversari='aniversari' ></cmp_Temps>
    </div>
  </q-page>
</template>

<style>
</style>

<script>

import cmp_Temps from 'components/temps';

export default {
  name: 'PageIndex',

  components:{cmp_Temps},

  data () {
  	return {
  		aniversaris: [
        // ***** IMPORTANT: ELS MESOS VAN DEL 0 AL 11 ********
        {nom: 'Clara',     dataNaix: new Date(2002,0,16,0,1,0)},
        {nom: 'Pol',       dataNaix: new Date(2000,0,31,0,1,0)},
        {nom: 'Gerard',    dataNaix: new Date(1997,3,22,0,1,0)},
        {nom: 'Jordi',     dataNaix: new Date(1968,3,25,0,1,0)},
        {nom: 'Bea',       dataNaix: new Date(1971,4,27,0,1,0)},
        {nom: 'Carlota',   dataNaix: new Date(2004,9,7,0,1,0)},
        {nom: 'Ana ',      dataNaix: new Date(1969,11,6,0,1,0)},
        {nom: 'Jose Luis', dataNaix: new Date(1972,11,19,0,1,0)},
  		]
  	}
  }
}
</script>
