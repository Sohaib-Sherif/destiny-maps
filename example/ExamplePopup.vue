<template>
  <example-wrapper title="DOM Elements / Popups">
    <template #description>
      <p>
        <a href="https://developers.google.com/maps/documentation/javascript/reference/overlay-view" target="_blank">DOM Elements</a> are basically anything you want to go on the
        map.
      </p>
      <p>They are not standard and have to be created from the google.maps.OverlayView class, which can be a little tricky.</p>
      <p>
        I made my own borderless InfoWindow with no close button (Popup) and you're encouraged to check out
        <a href="https://developers.google.com/maps/documentation/javascript/examples/overlay-popup" target="_blank">Google's example</a> of how to do this. Also check out my
        source code to see how I did it if you need to see how it's integrated.
      </p>
      <p>My popup class requires a 'position' property, and also takes background, height, and width properties.</p>
    </template>
    <template #map>
      <gmaps-map :options="mapOptions">
        <gmaps-popup :position="{ lat: -27.46, lng: 153.02 }" background="#BBF0FF">{{ text }}</gmaps-popup>
        <gmaps-popup :position="{ lat: -27.5, lng: 153.02 }" height="100px;">
          <button @click="text = 'Aussie Aussie Aussie'">Anything can</button><br />
          <button @click="text = 'Oi Oi Oi'">Go here</button>
        </gmaps-popup>
      </gmaps-map>
    </template>
    <template #code>
      <div>
        <pre>
&lt;gmaps-map>
  &lt;gmaps-popup
    :position="{ lat: -27.46, lng: 153.02 }"
    background="#BBF0FF">
    <span v-pre>{{ text }}</span>
  &lt;/gmaps-popup>

  &lt;gmaps-popup
    :position="{ lat: -27.5, lng: 153.02 }"
    height="100px;">
    &lt;button @click="text = 'Aussie Aussie Aussie'">
      Anything can
    &lt;/button>
    &lt;br />
    &lt;button @click="text = 'Oi Oi Oi'">
      Go here
    &lt;/button>
  &lt;/gmaps-popup>
&lt;/gmaps-map>

...

optionsA = { position: { lat: -27.46, lng: 153.02 } }
optionsB = { position: { lat: -27.5, lng: 153.02 } }

...

openB() {
  this.$refs.b.open()
}
          </pre>
      </div>
    </template>
  </example-wrapper>
</template>

<script>
import ExampleWrapper from './ExampleWrapper'
import { gmapsMap, gmapsPopup } from '../src' // import from 'x5-gmaps' for plugin

export default {
  name: 'ExamplePopup',
  components: { ExampleWrapper, gmapsMap, gmapsPopup },
  data: () => ({
    mapOptions: {
      center: { lat: -27.47, lng: 153.025 },
      zoom: 12,
      fullscreenControl: false,
      mapTypeControl: false,
      rotateControl: false,
      scaleControl: false,
      streetViewControl: false,
      zoomControl: false
    },
    text: 'This is just text'
  })
}
</script>
