<template>
  <div class="here-map">
    <div ref="map" v-bind:style="{ width: width, height: height }"></div>
  </div>
</template>

<script>
  export default {
    name: 'HereMap',
    props: {
      appId: String,
      ppCode: String,
      lat: String,
      lng: String,
      width: String,
      height: String,
    },
    data() {
      return {
        map: {
        },
        platform: {
        },
      }
    },
    created() {
      this.platform = new H.service.Platform({
        'app_id': this.appId,
        'app_code': this.appCode,
      });
    },
    mounted() {
      this.map = new H.Map(
        this.$refs.map,
        this.platform.createDefaultLayers().normal.map,
        {
          zoom: 10,
          center: {
            lng: this.lng,
            lat: this.lat,
          },
        }
      );
    },
  };
</script>

<style scoped></style>
