<template>
  <div class="here-map">
    <div id="mapContainer" ref="map" v-bind:style="{ width: width, height: height }"></div>
  </div>
</template>

<script>
  export default {
    name: 'HereMap',
    props: {
      width: String,
      height: String,
    },
    mounted() {
      // Initialize the platform object:
      var platform = new H.service.Platform({
        'app_id': 'PaDpEEql0MkSPo5SPhtC',
        'app_code': 'sZr2Yjat-uE8vMYdqyaR3w'
      });

      // Get the default map types from the Platform object:
      var defaultLayers = platform.createDefaultLayers();

      // Instantiate the map:
      var map = new H.Map(
              this.$refs.map,
              defaultLayers.normal.map,
              {
                zoom: 10,
                center: { lng: 30.29077658, lat: 59.99603261 }
              });

      // Create the default UI:
      var ui = H.ui.UI.createDefault(map, defaultLayers, 'ru-RU');

      var svgMarkup = '<svg width="44px" height="54px" viewBox="0 0 44 54" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">\n' +
              '    <!-- Generator: Sketch 53.1 (72631) - https://sketchapp.com -->\n' +
              '    <title>Group</title>\n' +
              '    <desc>Created with Sketch.</desc>\n' +
              '    <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">\n' +
              '        <g id="Group" transform="translate(1.000000, 1.000000)" stroke="#979797">\n' +
              '            <path d="M21,53 C21,53 42,29.1418885 42,18.7735456 C42,8.40520266 32.5979797,0 21,0 C9.40202025,0 0,8.40520266 0,18.7735456 C0,29.1418885 21,53 21,53 Z" id="Oval" fill="#D8D8D8"></path>\n' +
              '            <polygon id="Star" fill="#06C0F2" points="21.5 27 12.2423823 31.3262379 14.0104299 22.163119 6.52085987 15.6737621 16.8711911 14.336881 21.5 6 26.1288089 14.336881 36.4791401 15.6737621 28.9895701 22.163119 30.7576177 31.3262379"></polygon>\n' +
              '        </g>\n' +
              '    </g>\n' +
              '</svg>';

      var icon = new H.map.Icon(svgMarkup),
              coords = { lng: 30.29077658, lat: 59.99603261 },
              marker = new H.map.Marker(coords, {icon: icon});


      // Enable the event system on the map instance:
      var mapEvents = new H.mapevents.MapEvents(map);

      // Instantiate the default behavior, providing the mapEvents object:
      var behavior = new H.mapevents.Behavior(mapEvents);


      map.addEventListener('contextmenu', function(evt) {
        const geoPoint = map.screenToGeo(evt.viewportX, evt.viewportY);
        map.addObject(new H.map.Marker(geoPoint, {icon: icon}));
        console.log(map.screenToGeo(evt.viewportX, evt.viewportY));
      });

      map.addObject(marker);
      map.setCenter(coords);
    },
  };
</script>

<style scoped></style>
