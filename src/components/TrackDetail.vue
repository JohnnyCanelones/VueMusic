<template lang="pug">
 .container
  pm-loader(v-if="isLoading")
  .columns(v-if="track && track.id")
    .column.is-3.has-text-centered
      figure.media-left
        p.image
          img(:src="track.album.images[0].url")
        br
        p
          a.button.is-primary.is-large
            span.icon(@click="selectTrack") ▶️
    .column.is-8
      .panel
        .panel-heading
          h1.title {{ trackTitle }}
        .panel-block
          article.media
            .media-content
              .content
                ul(v-for="(value, key) in track")
                  li
                    strong {{ key }}:&nbsp;
                    span {{ value }} 
              
              nav.level
                .level-left
                  a.level-item
</template>

<script>
import { mapState, mapActions, mapGetters } from 'vuex'
import PmLoader from '@/components/shared/Loader.vue'
import trackMixin from '@/mixins/track'

  export default {
    mixins: [ trackMixin ],
   components: { PmLoader },
   data() {
     return {
        isLoading: true,
     }
   },
   computed: {
     ... mapState(['track']),
     ... mapGetters(['trackTitle'])
   },
   
   created() {
     this.isLoading = true
     const id = this.$route.params.id
    if (!this.track || !this.track.id || this.track.id != id) {
      this.getTrackById({ id })
      .then(()=> {
        console.log('Track Loaded')
        this.isLoading = false

      })

    }else{

      this.isLoading = false
    }

    
   },

   methods: {
     ... mapActions(['getTrackById'])
   },
  }
</script>

<style lang="scss" scoped>
  .columns {
    margin: 20px;
  }
</style>