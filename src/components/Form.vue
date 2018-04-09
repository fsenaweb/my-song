<template>
  <v-content>
    <v-container fluid fill-height>
      <v-layout justify-center>
        <v-flex xs12 sm8 md8>
          <v-card class="elevation-2">
            <v-form class="ma-2">
              <v-text-field
                label="Artista"
                v-model="artist"
                required
              ></v-text-field>
              <v-text-field
                label="Música"
                v-model="music"
                required
              ></v-text-field>
            </v-form>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn depressed small color="primary" @click.prevent="findMusic">Pesquisar</v-btn>
            </v-card-actions>
          </v-card>
          <v-card class="elevation-2 mt-3">
            {{ result }}

            <v-card-actions>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </v-content>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'Form',
    data () {
      return {
        artist: '',
        music: '',
        result: ''
      }
    },
    methods: {
      findMusic () {
        axios.get('https://api.vagalume.com.br/search.php?art=' + this.artist + '&mus=' + this.music + '&apikey={bcd3ff0cd991b534b5c2038f183788c2}')
          .then(response => {
            // JSON responses are automatically parsed.
            this.result = response.data
            console.log(this.result)
          })
          .catch(e => {
            this.errors.push(e)
          })
      }
    }
  }
</script>

<style scoped>

</style>
