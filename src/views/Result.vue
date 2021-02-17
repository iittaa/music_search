<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          検索結果
        </h1>
        <p>検索キーワード：{{ $route.params.keyword }}</p>
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col class="mb-4" style="margin-bottom: 10px;" v-for="(album, i) in albums" :key="i">
        <v-card
          color="pink"
          opacity="0.1"
          dark 
          :href="album.collectionViewUrl"
        >
          <div class="d-flex flex-no-wrap justify-space-between">
            <div>
              <v-card-title
                class="headline"
                v-text="album.collectionName"
                
              ></v-card-title>

              <v-card-subtitle v-text="album.artistName"></v-card-subtitle>

              <v-card-actions>
                <v-btn
                  class="ml-2 mt-3"
                  fab
                  icon
                  height="40px"
                  right
                  width="40px"
                >
                  <v-icon>mdi-play</v-icon>
                </v-btn>

                <v-btn
                  class="ml-2 mt-5"
                  outlined
                  rounded
                  small
                >
                  START RADIO
                </v-btn>
              </v-card-actions>
            </div>

            <v-avatar
              class="ma-3"
              size="125"
              tile
            >
              <v-img :src="album.artworkUrl100"></v-img>
            </v-avatar>
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios"

export default {
  data() {
    return {   
      albums: [],
    }
  },
  created() {
    const vm = this
    // jsonをサーバーから取得している
    axios.get(`https://itunes.apple.com/search?term=${this.$route.params.keyword}&entity=album&lang=ja_jp&country=jp&limit=10`)
    // responseは取得して受け取ったもの
    .then((response) => {
      console.log(response)
      vm.albums = response.data.results
    })
  }
}
</script>

