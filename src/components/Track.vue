<template lang="pug">
  .card(v-if="track && track.album")
    .card-image
      figure.image.is3by1
        img(:src="track.album.images[0].url")
    
    .card-content
      .media
        .media-left
          figure.image.is-48x48
            img(:src="track.album.images[0].url")

        .media-content
          p.title.is-6
            strong {{track.name}} 
          p.subtitle.is-6
            strong {{track.artists[0].name}}
      
      .content
        small {{track.duration_ms | ms-to-mm}}
        .level
          .level-left
            button.button.is-primary.level-item
              span.icon.is-small(@click="selectTrack") ▶
          .level-right
            button.button.is-warning.level-item()
              span.icon.is-small(@click="goToTrack(track.id)") 🌎
              

</template>

<script>
import trackMixin from '@/mixins/track'

  export default {
  mixins: [ trackMixin ],
    props:{
      track: {
        type: Object,
        required: true,
      }
    },
    methods: {
      

      goToTrack(id) {
        if (!this.track.preview_url) { return }
        this.$router.push({ name: 'track', params: { id } })        
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>