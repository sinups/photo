<template>
 
    <v-layout row wrap>
     <v-flex xs3 v-for="photo in photos" v-bind:key="photo">
       <v-img
          :src="photo.urls.regular"  height="250px"
          gradient="to top right, rgba(100,115,201,.33), rgba(25,32,72,.7)"
        ></v-img>
        <v-card dark color="secondary">
          <v-card-text class="px-0"><a :href="photo.user.portfolio_url" target="_blank">{{ photo.user.name }}</a></v-card-text>
        </v-card>
      </v-flex>
   
    </v-layout>
 
</template>
<script>
export default {
   data () {
    return {
      photos: [],
      totalPhotos: 0,
      perPage: 50,
      currentPage: 1
    }

  },
  methods: {
    fetchPhotos: function(page) {
      var options = {
        params: {
          client_id: appId,
          page: page,
          per_page: this.perPage
        }
      }

      this.$http.get('https://api.unsplash.com/photos', options).then(function(response) {
        console.log(response);
        this.photos = response.data

        this.totalPhotos = parseInt(response.headers.get('x-total'))

        this.currentPage = page
        

      }, console.log)
    }
  },
  created: function() {
    this.fetchPhotos(this.currentPage)
  }
}
</script>
