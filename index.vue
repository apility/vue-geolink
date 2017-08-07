<template>
  <div @click="open($event)">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    props: ['lat', 'lng', 'zoom', 'label', 'address'],
    methods: {
      open (e) {
        if (!this.address && (!this.lat || !this.lng)) {
          return
        }
        let isApple = /(iPad)|(iPhone)|(iPod)/i.test(navigator.userAgent)
        this.zoom = parseInt(!this.zoom ? 12 : this.zoom)
        this.label = !this.label ? `${this.lat},${this.lng}` : this.label
        let androidURL = false
        let appleURL = false
        if (this.address && !(this.lat || this.lng)) {
          androidURL = `https://www.google.com/maps/place/${this.address}`
          appleURL = `https://maps.apple.com/?q=${this.address}`
        }
        if (!this.address && (this.lat && this.lng)) {
          androidURL = `https://www.google.com/maps/place/${this.label}/@${this.lat},${this.lng},${this.zoom}z`
          appleURL = `https://maps.apple.com/?q=${this.label}&ll=${this.lat},${this.lng}&z=${this.zoom}`
        }
        if (androidURL || appleURL) {
          e.preventDefault()
          window.open(!isApple ? androidURL : appleURL)
          return false
        }
      }
    }
  }
</script>
