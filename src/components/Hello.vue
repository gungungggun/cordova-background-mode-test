<template lang="pug">
  main
    p {{ count }}
</template>

<script>
export default {
  data () {
    return {
      count: 0
    }
  },
  mounted () {
    document.addEventListener('deviceready', this.onDeviceReady, false)
  },
  methods: {
    onDeviceReady () {
      cordova.plugins.backgroundMode.enable()
      cordova.plugins.backgroundMode.on('enable', () => {
        setInterval(this.loop, 1000)
      })
    },
    loop () {
      this.count++
      if (this.count === 100)  {
        cordova.plugins.backgroundMode.moveToForeground()
      }
      if (this.count === 150) {
        cordova.plugins.backgroundMode.moveToBackground()
      }
    }
  }
}
</script>
