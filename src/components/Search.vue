<template>
  <div id="main">
    <transition name="move">
      
      <pm-notification v-show="showNotification" :isSucceed="isSucceed">
        <p slot="body" v-if="isSucceed">
          {{ searchMessages }}
        </p>
        <p slot="body" v-else>
          No se encontraron resultados
        </p>
      </pm-notification>
    </transition>

   
    <section class="section" >
      <nav class="has-shadow">
        <div class="container">
          <div class="colunms">
            <div class="field has-addons column is-5 is-offset-4">
              <div class="control">
                <input type="text" class="input  is-medium " placeholder="Buscar Canciones" v-model="searchQuery" @keyup.enter="search">
              </div>
              <div class="control">
                  <button  @click='search' class="button is-info is-primary is-medium"> Buscar</button>
              </div>
              <div class="control is-info">
                  <button href="" class="button is-danger  is-medium is-warning">&times;</button>
              </div>
            </div>
          </div>
        </div>
      <div class="container encontrados ">
          <div class="colunms">
            <p class="small column is-5 is-offset-4 ">{{ searchMessages }} </p>

          </div>
        </div>
      </nav>
    
    <transition name="move">
      
      <pm-loader v-show="isLoading" ></pm-loader>
    </transition>

      <div class="container" v-show="!isLoading">
        <div class="columns is-multiline">
          
          <div  class="column is-one-quarter" v-for="track in tracks">
              <pm-track
                v-blur="track.preview_url" 
                :class="{'is-active': track.id == selectedTrack}"
                :track="track"
                @select="setSelectedTrack" >
                </pm-track>
              
          </div>      
        </div>

      </div>
    </section>

  </div> 
</template>

<script>
import trackService from '@/services/track';
import PmTrack from '@/components/Track.vue'
import PmLoader from '@/components/shared/Loader.vue'
import PmNotification from '@/components/shared/Notification.vue'
export default {
  name: 'app',
  data () {
    return {
      searchQuery: '',
      tracks: [],
      isLoading: false,
      showNotification: false,
      isSucceed: false, 

      selectedTrack: '',
     }
  },
  computed: {
    searchMessages() {
      return `Encontrados: ${this.tracks.length} `    
    }
  },
  methods: {
    search () {
      if (!this.searchQuery ) { return }
      this.isLoading = true
      trackService.search(this.searchQuery)
        .then( res => {
          if (res.tracks.total === 0) {
            this.isSucceed = false 
            
          }else {
            this.isSucceed = true 
            
          }
         
          // console.log(res.tracks.total)
          this.isLoading = false
          this.tracks = res.tracks.items
          this.showNotification = true

        })
    },

    setSelectedTrack (id) {
      this.selectedTrack = id
    }
    
  },
  components:{ PmTrack, PmLoader, PmNotification},

  watch: {
    showNotification() {
      if(this.showNotification) {
        setTimeout(() => {
          this.showNotification = false
        }, 3000);
      }
    }
  },
  
}
</script>

<style lang="scss" scoped>

 .encontrados {
   margin-bottom: 25px;
   margin-top: 10px;
 }

 .is-active {
   border: 2px #23d160 solid
 }

</style>
