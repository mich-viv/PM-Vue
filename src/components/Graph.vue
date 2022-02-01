<template>
	<div>
		<canvas id="chart"></canvas>
		<p id="tki">{{trek}}</p>
	</div>
	
</template>

<script>

import Chart from 'chart.js'
import axios from 'axios'

export default {
  name: 'Graph',
  props: ['trek'],
  data() {
    return {
      chart: null,
      GraphData: ''
    }
  },
  updated() {
    if(this.chart!==null){
    this.chart.destroy();
    }

  axios.get('../sentiero_'+this.$props.trek+'.gpx', { responseType: 'document' }).then(response => {
		
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

	
	
	//distanza tra due generici punti date le coordinate P1:(lat,lon) e P2:(lat,lon) 
	for (i = 1; i < elev.length; i++) {
			
			dist.push(haversine(lat[i - 1], lon[i - 1], lat[i], lon[i]).toFixed(2));
		
	} //for
	
  //inizializzo dist_parziali

	dist_parziali[0] = 0;
	
	for (var k = 1; k < elev.length; k++) {
		var s = 0;
	
		for (var j = 0; j < k; j++) {
			s += parseInt(dist[j]);
		} //for-j

	dist_parziali[k] = Number((s / 1000).toFixed(2));
	} //for-k


		//distanza totale
   
    
  this.GraphData = {
    type: "bar",
    data: {
      labels: dist_parziali,
      datasets: [
        {
          label: "Altimetria "+this.$props.trek,
          data: elev,
          backgroundColor: "rgba(54,73,93,.5)",
          borderColor: "#36495d"
        }
      ]
    },
    options: {
      responsive: true,
      tooltips: {
        displayColors: false,
        callbacks: {
          label: function label(tooltipItem) {
            return "Altitudine: " + tooltipItem.yLabel;
          },
          title: function title() {
            return "";
          }
        } 

      }
    }
   };
   const ctx = document.getElementById('chart');
   this.chart = new Chart(ctx, this.GraphData);
	});

  
    
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#tki{
  visibility: hidden;

}
</style>
