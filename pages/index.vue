<template>
  <v-layout>
    <v-row>
      <v-col cols="12" class="py-0">
        <no-ssr>
          <l-map :zoom="7.5" :center="center" :options="leafletMapOptions">
            <l-tile-layer
              url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"
            ></l-tile-layer>
            <!-- <l-geo-json
              v-if="show"
              :geojson="geojson"
              :options="options"
              :options-style="styleFunction"
            /> -->
            <l-geo-json v-if="show" :geojson="geojson" />
            <l-marker :lat-lng="[55.9464418, 8.1277591]"></l-marker>
          </l-map>
        </no-ssr>
      </v-col>
    </v-row>
  </v-layout>
</template>

<script>
export default {
  components: {},
  data: () => ({
    loading: false,
    show: true,
    enableTooltip: true,
    zoom: 6,

    center: [32.612855, -89.902802],
    geojson: null,
    fillColor: '#e4ce7f',
    url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
    leafletMapOptions: {
      closePopupOnClick: false,
      doubleClickZoom: 'center',
      zoomDelta: 0.25,
    },
  }),
  async created() {
    this.loading = true
    const response = await fetch(
      'https://raw.githubusercontent.com/davidbkay/precinct-map/main/static/precincts.json'
    )
    const data = await response.json()
    this.geojson = data
    this.loading = false
  },
}
</script>
