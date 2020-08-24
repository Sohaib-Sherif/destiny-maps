<template>
  <div class="gmaps-popup-container" @click.prevent="$emit('click')">
    <div class="gmaps-popup-bubble-anchor" :style="`color: ${background};`">
      <div class="gmaps-popup-bubble" :style="`background: ${background}; maxWidth:${width}; maxHeight:${height};`">
        <slot />
      </div>
    </div>
  </div>
</template>

<script>
import createPopupClass from './popupClass.js'

export default {
  name: 'gmapsPopup',
  inject: ['getMap', 'handleError'],
  props: {
    background: { type: String, default: '#EEEEEE' },
    width: { type: String, default: '200px' },
    height: { type: String, default: '60px' },
    position: { type: Object, required: true },
    xOffset: {type: Number, default: 0},
    yOffset: {type: Number, default: 0}
  },
  data: () => ({ popup: null }),
  watch: {
    position(pos) {
      this.popup.setPosition(pos)
    }
  },
  mounted() {
    const Popup = createPopupClass()
    this.$GMaps()
      .then(GMaps => (this.popup = new Popup(this.position, this.$el, this.xOffset, this.yOffset ,GMaps)))
      .then(() => this.popup.setMap(this.getMap()))
      .catch(e => this.handleError(e))
  },
  beforeDestroy() {
    if (this.popup) this.popup.setMap(null)
  }
}
</script>
