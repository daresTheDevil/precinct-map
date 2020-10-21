<template>
  <v-layout>
    <v-row>
      <v-col cols="12" class="py-0">
        <no-ssr>
          <l-map
            :zoom="13"
            :center="[55.9464418, 8.1277591]"
            :options="leafletMapOptions"
          >
            <l-tile-layer
              url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"
            ></l-tile-layer>
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
    leafletMapOptions: {
      closePopupOnClick: false,
      doubleClickZoom: 'center',
      zoomDelta: 0.25,
    },
  }),
}
</script>
