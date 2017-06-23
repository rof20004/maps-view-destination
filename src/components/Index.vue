<template>
  <q-layout>
    <div slot="header" class="toolbar">
      <q-toolbar-title :padding="0">
        Maps View Destination
      </q-toolbar-title>
    </div>

    <div class="layout-view">
      <div class="layout-padding">
        <vue-google-autocomplete
            id="map"
            classname="full-width"
            placeholder="Informe o destino"
            v-on:placechanged="getAddressData"
            country="br"
            :enable-geolocation="true"
            :enableGetCurrentAddress="true"
            @getCurrentAddress="currentAddress = $event">
        </vue-google-autocomplete>
        <br><br>
        <div id="map-area">
          <iframe id="map" scrolling="no" frameborder="0" style="border:0" :src="`https://maps.google.com/maps?saddr=${this.currentAddress}&daddr=${this.address}&output=embed`" allowfullscreen></iframe>
        </div>
      </div>
    </div>
  </q-layout>
</template>

<script>
import VueGoogleAutocomplete from 'vue-google-autocomplete'

export default {
  components: { VueGoogleAutocomplete },
  data () {
    return {
      address: '',
      currentAddress: ''
    }
  },
  methods: {
    getAddressData (addressData, placeResultData) {
      this.address = placeResultData.formatted_address
    }
  }
}
</script>

<style scoped>
iframe {
  width: 100% !important;
  height: calc(100vh - 200px) !important;
}
</style>
