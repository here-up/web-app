<template>
  <div class="here-map">
    <div id="mapContainer" ref="map" v-bind:style="{ width: width, height: height }"></div>
  </div>
</template>

<script>
  import { JsonRpc } from "eosjs";
  const rpc = new JsonRpc("https://jungle2.cryptolions.io:443", { fetch });

  export default {
    name: 'HereMap',
    props: {
      width: String,
      height: String,
    },
    async mounted() {
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

      var svgMarkup = '<svg\n' +
              '   xmlns:dc="http://purl.org/dc/elements/1.1/"\n' +
              '   xmlns:cc="http://creativecommons.org/ns#"\n' +
              '   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"\n' +
              '   xmlns:svg="http://www.w3.org/2000/svg"\n' +
              '   xmlns="http://www.w3.org/2000/svg"\n' +
              '   id="svg8"\n' +
              '   version="1.1"\n' +
              '   viewBox="0 0 156.16449 198.43854"\n' +
              '   height="54px"\n' +
              '   width="44px">\n' +
              '  <defs\n' +
              '     id="defs2" />\n' +
              '  <metadata\n' +
              '     id="metadata5">\n' +
              '    <rdf:RDF>\n' +
              '      <cc:Work\n' +
              '         rdf:about="">\n' +
              '        <dc:format>image/svg+xml</dc:format>\n' +
              '        <dc:type\n' +
              '           rdf:resource="http://purl.org/dc/dcmitype/StillImage" />\n' +
              '        <dc:title></dc:title>\n' +
              '      </cc:Work>\n' +
              '    </rdf:RDF>\n' +
              '  </metadata>\n' +
              '  <g\n' +
              '     transform="translate(-27.75122,-24.478092)"\n' +
              '     id="layer1">\n' +
              '    <path\n' +
              '       transform="scale(0.26458333)"\n' +
              '       id="rect3719"\n' +
              '       d="m 400.00391,92.515625 a 294.99664,294.99664 0 0 0 -294.99805,294.996095 294.99664,294.99664 0 0 0 0,0.0176 l -0.006,-0.01 c 0,0 -1.107,16.0986 3.59766,44.35352 a 294.99664,294.99664 0 0 0 9.375,41.22265 C 142.06287,557.6588 209.94695,695.38168 400,842.51953 586.17851,698.38133 655.1114,563.28521 680.49219,478.33984 a 294.99664,294.99664 0 0 0 9.96093,-41.04296 c 1.38787,-7.56715 2.37954,-14.37525 3.07227,-20.33399 a 294.99664,294.99664 0 0 0 0,-0.0117 C 695.72521,398.02198 695,387.51953 695,387.51953 a 294.99664,294.99664 0 0 0 0,-0.008 A 294.99664,294.99664 0 0 0 400.00391,92.515625 Z"\n' +
              '       style="display:inline;fill:#363636;fill-opacity:1;stroke-width:0.84089625" />\n' +
              '    <path\n' +
              '       id="path4536"\n' +
              '       transform="scale(0.26458333)"\n' +
              '       d="m 267.76562,722.51953 c 35.70681,38.63461 79.2112,78.94979 132.23438,120 53.02412,-41.05093 96.52608,-81.36557 132.23242,-120 z"\n' +
              '       style="fill:#65c1c2;fill-opacity:1;stroke-width:0.84089625" />\n' +
              '    <path\n' +
              '       transform="scale(1,-1)"\n' +
              '       d="M 105.83333,-52.260414 91.3693,-81.567736 59.026752,-86.267381 82.43004,-109.07995 l -5.524768,-32.21186 28.928058,15.20837 28.92805,-15.20837 -5.52476,32.21186 23.40329,22.812566 -32.34255,4.699649 z"\n' +
              '       id="path4534"\n' +
              '       style="display:inline;opacity:1;fill:#65c1c2;fill-opacity:1;stroke-width:0;stroke-miterlimit:4;stroke-dasharray:none" />\n' +
              '  </g>\n' +
              '  <g\n' +
              '     transform="translate(-27.75122,-24.478092)"\n' +
              '     style="display:inline"\n' +
              '     id="layer2" />\n' +
              '</svg>\n';

      var icon = new H.map.Icon(svgMarkup);
              // coords = { lng: 30.29077658, lat: 59.99603261 },
              // marker = new H.map.Marker(coords, {icon: icon});

      const coordinates = (await rpc.get_table_rows({
        json: true,
        code: 'hereherehere',
        scope: 'heretokentst',
        table: 'coordinate'
      })).rows.map(r => ({lat: r.latitude, lng: r.longitude}));

      coordinates.forEach(c => map.addObject(new H.map.Marker(c, {icon})));

      // Enable the event system on the map instance:
      var mapEvents = new H.mapevents.MapEvents(map);

      // Instantiate the default behavior, providing the mapEvents object:
      var behavior = new H.mapevents.Behavior(mapEvents);


      map.addEventListener('contextmenu', function(evt) {
        const geoPoint = map.screenToGeo(evt.viewportX, evt.viewportY);
        map.addObject(new H.map.Marker(geoPoint, {icon}));
        console.log(map.screenToGeo(evt.viewportX, evt.viewportY));
      });
    },
  };
</script>

<style scoped></style>
