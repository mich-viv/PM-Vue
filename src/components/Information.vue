<template>
  <div :class="{invisible: !value1}" class="mt-5 text-center">
	<p id="tki" v-on:change="selectedTrek">{{trek}}</p>
	<p>distanza totale: <strong>{{length}}</strong></p>
	<p>quota massima: <strong>{{max}}</strong></p>
	<p>quota minima: <strong>{{min}}</strong></p>
	
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'Information',
  props: ['trek','info','length','max','min'],
  
  computed: {
	selectedTrek(){
		return "information: "+this.$props.trek;
  },

  data () {
    return {
		value1: false,
		info: null,
		length: null,
		max: null,
		min: null
    }
  },
  methods: {
	//test
  }
},

updated() {

	axios.get('../sentiero_'+this.$props.trek+'.gpx', { responseType: 'document' }).then(response => {
		this.value1=true;
		
		var xinf=response.data.getElementsByTagName("trkpt");
		var elev = [];
		var lat = [];
		var lon = [];
		
	function haversine(la1, lo1, la2, lo2){
		var lat1 = (la1 / 180.0 * 3.14159);
		var lon1 = (lo1 / 180.0 * 3.14159);
		var lat2 = (la2 / 180.0 * 3.14159);
		var lon2 = (lo2 / 180.0 * 3.14159);
		var R = 6372.8; // km
	
		var dLat = lat2 - lat1;
		var dLon = lon2 - lon1;
		var a = (Math.sin(dLat / 2) * Math.sin(dLat / 2) + Math.sin(dLon / 2) * Math.sin(dLon / 2) * Math.cos(lat1) * Math.cos(lat2));
		var c = (2 * Math.asin(Math.sqrt(a)));
		return (R * c * 1000);
	}

	for (var i = 0; i < xinf.length; i++) {
		lat.push(xinf[i].getAttribute('lat'));
		lon.push(xinf[i].getAttribute('lon'));
		elev.push(xinf[i].getElementsByTagName('ele')[0].childNodes[0].nodeValue);
		
	} //for
	

	var dist = []; //array contenente all'indice i la distanze dal punto xi al punto xi+1
	
	var dist_parziali = []; //array contenente la ripartizione delle somme di tutte le distanze antecedenti a xi, serve per la scala X del grafico 
	
	var tot = 0; //distanza complessiva
		
	var min = elev[0]; //elevazione minima
		
	var max = elev[0]; //elevazione massima

	for (i = 1; i < elev.length; i++) {
		dist.push(haversine(lat[i - 1], lon[i - 1], lat[i], lon[i]));
		if (max < elev[i]) {
		max = elev[i];
		} //if
	
	
		if (min > elev[i]) {
		min = elev[i];
		} //if-else
	
	} //for
	dist_parziali[0] = 0;

	for (var k = 1; k < elev.length; k++) {
		var s = 0;

		for (var j = 0; j < k; j++) {
			s += dist[j];
		} //for-j


	dist_parziali[k] = Number((s / 1000).toFixed(2));
	} //for-k

	for (var u = 0; u < dist.length; u++) {
		tot+= dist[u];
	} //for-u

	this.length=Number((tot / 1000).toFixed(2)) + " KM; ";
	this.max=max + " m; ";
	this.min=min + " m; ";
	});

		
	}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.invisible {
    visibility: hidden;
}
#tki{
	visibility: hidden;
}
</style>
