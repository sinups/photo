<template>
  <v-app>
    <v-content>
      <appheader />
    </v-content>
    <template>
      <template>
        <v-layout row wrap  pa-3 mb-2>
          
          <v-flex xs12 sm6 md3    pa-1 mb-1 v-for="photo in photos" :key="photo.id">
            <v-img :src="photo.urls.regular" height="250px"></v-img>
            <v-card>
              <v-card-actions>
                <v-list-tile class="grow">
                  <v-list-tile-avatar color="grey darken-3">
                    <v-img class="elevation-6" :src="photo.user.profile_image.small"></v-img>
                  </v-list-tile-avatar>

                  <v-list-tile-content>
                    <v-list-tile-title>{{ photo.user.name }}</v-list-tile-title>
                  </v-list-tile-content>

                  <v-layout align-center justify-end>
                    <v-btn icon>
                      <v-icon>favorite</v-icon>
                    </v-btn>
                    <v-btn icon>
                      <v-icon>bookmark</v-icon>
                    </v-btn>
                    <v-btn icon>
                      <v-icon>share</v-icon>
                    </v-btn>
                  </v-layout>
                </v-list-tile>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </template>
    </template>
    <div class="text-xs-center">
      <pagination
        :current="currentPage"
        :total="totalPhotos"
        :per-page="perPage"
        @page-changed="fetchPhotos"
      ></pagination>
    </div>
  </v-app>
</template>

<script>
import appheader from "./components/appheader";
// import cards from './components/cards';
import pagination from "./components/pagination";
import { log } from "util";
var appId = "96f61dc28430b0c51088e051a42c22190cbb0718a6f9c9eab25315a2ad589d2a";

export default {
  name: "App",
  components: {
    appheader,
    pagination
    // cards
  },
  data() {
    return {
      photos: [],
      totalPhotos: 0,
      perPage: 20,
      currentPage: 1
    };
  },
  methods: {
    fetchPhotos: function(page) {
      var options = {
        params: {
          client_id: appId,
          page: page,
          per_page: this.perPage
        }
      };

      this.$http
        .get("https://api.unsplash.com/photos", options)
        .then(function(response) {
          console.log(response);
          this.photos = response.data;

          this.totalPhotos = parseInt(response.headers.get("x-total"));

          this.currentPage = page;
        }, console.log);
    }
  },
  created: function() {
    this.fetchPhotos(this.currentPage);
  }
};
</script>
