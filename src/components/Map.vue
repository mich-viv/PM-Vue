<template>
  <div ref="map-root" style="width: 100%; height: 100%">
  </div>
</template>

<script>
  import View from 'ol/View'
  import Map from 'ol/Map'
  import TileLayer from 'ol/layer/Tile'
  import OSM from 'ol/source/OSM'
  import GPX from 'ol/format/GPX'
  import VectorLayer from 'ol/layer/Vector'
  import VectorSource from 'ol/source/Vector'
  import {Circle as CircleStyle, Fill, Stroke, Style} from 'ol/style';
  import {useGeographic} from 'ol/proj';
  import 'ol/ol.css'
	
  export default {
    name: 'MapContainer',
    components: {},
    props: {},
	
	mounted() {
		useGeographic();

      var cai560 = [12.0689022, 46.3992571];
      var cai567 = [11.9810255, 46.3612238];
      var cai483 = [12.3167969, 46.3337943];
      var cai215 = [12.2044485, 46.5562143];
      var cai762 = [11.9180211, 46.3041354];
      var cai333 = [11.63223, 46.2366298];
      var cai334 = [11.6235375, 46.2160783];
      var cai764 = [11.966388, 46.336861];
      var view_reset =  [12.05,46.3833];
      
      const style = {
        'Point': new Style({
          image: new CircleStyle({
            fill: new Fill({
              color: 'rgba(255,255,0,0.8)',
            }),
            radius: 5,
            stroke: new Stroke({
              color: '#000',
              width: 1,
            }),
          }),
        }),
        'LineString': new Style({
          stroke: new Stroke({
            color: '#f00',
            width: 3,
          }),
        }),
        'MultiLineString': new Style({
          stroke: new Stroke({
            color: '#f00',
            width: 3,
          }),
        }),
      };

      var vector1 = new VectorLayer({
        source: new VectorSource({
          url: '../sentiero_215.gpx',
          format: new GPX(),
        }),
        style: function (feature) {
          return style[feature.getGeometry().getType()];
        },
      });

      var vector2 = new VectorLayer({
        source: new VectorSource({
          url: '../sentiero_333.gpx',
          format: new GPX(),
        }),
        style: function (feature) {
          return style[feature.getGeometry().getType()];
        },
      });

      var vector3 = new VectorLayer({
        source: new VectorSource({
          url: '../sentiero_334.gpx',
          format: new GPX(),
        }),
        style: function (feature) {
          return style[feature.getGeometry().getType()];
        },
      });

      var vector4 = new VectorLayer({
        source: new VectorSource({
          url: '../sentiero_483.gpx',
          format: new GPX(),
        }),
        style: function (feature) {
          return style[feature.getGeometry().getType()];
        },
      });

      var vector5 = new VectorLayer({
        source: new VectorSource({
          url: '../sentiero_560.gpx',
          format: new GPX(),
        }),
        style: function (feature) {
          return style[feature.getGeometry().getType()];
        },
      });

      var vector6 = new VectorLayer({
        source: new VectorSource({
          url: '../sentiero_567.gpx',
          format: new GPX(),
        }),
        style: function (feature) {
          return style[feature.getGeometry().getType()];
        },
      });

      var vector7 = new VectorLayer({
        source: new VectorSource({
          url: '../sentiero_762.gpx',
          format: new GPX(),
        }),
        style: function (feature) {
          return style[feature.getGeometry().getType()];
        },
      });

      var vector8 = new VectorLayer({
        source: new VectorSource({
          url: '../sentiero_764.gpx',
          format: new GPX(),
        }),
        style: function (feature) {
          return style[feature.getGeometry().getType()];
        },
      });


      var raster = new TileLayer({
        source: new OSM(),
      });

      var view = new View({
        center: [12.05,46.3833],
        zoom: 10,
        constrainResolution: true
      });

      new Map({
        target: this.$refs['map-root'],
        layers: [raster,vector1,vector2,vector3,vector4,vector5,vector6,vector7,vector8],
        // coordinata centrale sulle dolomiti
        view: view,
      });

      this.$root.$on('click', item =>{
        if(item==true){
          view.animate({
            center: view_reset,
            zoom: 10,
            duration: 2000
          });
        }//if
      });

      this.$root.$on('change', item => {
        if(item==560){
          view.animate({
            center: cai560,
            zoom: 15,
            duration: 2000
          });
        }else if(item==567){
          view.animate({
            center: cai567,
            zoom: 15,
            duration: 2000
          });
          
        }else if(item==483){
          view.animate({
            center: cai483,
            zoom: 15,
            duration: 2000
          });

        }else if(item==215){
          view.animate({
            center: cai215,
            zoom: 15,
            duration: 2000
          });

        }else if(item==762){
          view.animate({
            center: cai762,
            zoom: 15,
            duration: 2000
          });

        }else if(item==333){
          view.animate({
            center: cai333,
            zoom: 15,
            duration: 2000
          });

        }else if(item==764){
          view.animate({
            center: cai764,
            zoom: 15,
            duration: 2000
          });

        }else if(item==334){
          view.animate({
            center: cai334,
            zoom: 15,
            duration: 2000
          });

        }//if-else
      });
    },
  }
</script>
