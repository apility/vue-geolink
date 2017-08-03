<template>
  <div @click.prevent="open">
    <slot></slot>
  </div> </template> <script>
  export default {
    props: ['lat', 'lng', 'zoom', 'label'],
    methods: {
      open () {
        if (!this.lat || !this.lng) {
          return
        }
        let isApple = /(iPad)|(iPhone)|(iPod)/i.test(navigator.userAgent)
        this.zoom = parseInt(!this.zoom ? 12 : this.zoom)
        this.label = !this.label ? `${this.lat},${this.lng}` : this.label
        let androidURL = `https://www.google.com/maps/place/${this.label}/@${this.lat},${this.lng},${this.zoom}z`
        let appleURL = `https://maps.apple.com/?q=${this.label}&ll=${this.lat},${this.lng}&z=${this.zoom}`
        window.open(!isApple ? androidURL : appleURL)
      }
    }
  }
</script>
