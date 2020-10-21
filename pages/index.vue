<template>
  <v-layout>
    <v-row>
      <v-col cols="12" class="py-0">
        <client-only>
          <l-map
            ref="map"
            :zoom="zoom"
            :center="center"
            :options="leafletMapOptions"
          >
            <!-- <l-tile-layer
              url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"
            ></l-tile-layer> -->
            <!-- <l-geo-json
              v-if="show"
              :geojson="geojson"
              :options="options"
              :options-style="styleFunction"
            /> -->
            <l-geo-json ref="geoJson" v-if="show" :geojson="geojson" />
            <l-marker :lat-lng="[55.9464418, 8.1277591]"></l-marker>
          </l-map>
        </client-only>
      </v-col>
    </v-row>
  </v-layout>
</template>

<script>
export default {
  components: {},
  async fetch() {
    this.geojson = await fetch(
      'https://raw.githubusercontent.com/davidbkay/precinct-map/main/static/precincts.json'
    ).then((res) => res.json())
  },
  data: () => ({
    loading: false,
    show: true,
    enableTooltip: true,
    zoom: 7.5,
    center: [32.612855, -89.902802],
    geojson: null,
    fillColor: '#e4ce7f',
    url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
    leafletMapOptions: {
      closePopupOnClick: false,
      doubleClickZoom: 'center',
      zoomDelta: 0.25,
      zoomSnap: 0,
    },
  }),
  computed: {
    initZoom() {
      if (this.$vuetify.breakpoint.smAndDown) return 6
      return 7.5
    },
  },
  methods: {
    zoomToState() {
      console.log('map', this.$refs.map)
      console.log('geojson', this.$refs.geoJson)
      // this.$refs.map.fitBounds(this.$refs.geoJson.mapObject.getBounds())
    },
  },
  updated() {
    this.$nextTick(() => {
      this.zoomToState()
    })

    // this.loading = true
    // const response = await fetch(
    //   'https://raw.githubusercontent.com/davidbkay/precinct-map/main/static/precincts.json'
    // )
    // const data = await response.json()
    // this.geojson = data
    // this.loading = false
    // this.$refs.map.fitBounds(this.$refs.geojson.getBounds())
  },
}
</script>
