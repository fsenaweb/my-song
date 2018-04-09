<template>
  <v-content>
    <v-container fluid fill-height>
      <v-layout justify-center>
        <v-flex xs12 sm8 md8>
          <v-card class="elevation-2">
            <v-form  @submit.prevent="findMusic" class="ma-2">
              <v-text-field
                label="Artista"
                v-model="txtartist"
                required
              ></v-text-field>
              <v-text-field
                label="Música"
                v-model="txtmusic"
                required
              ></v-text-field>
            </v-form>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn depressed small color="primary" @click.prevent="findMusic">Pesquisar</v-btn>
            </v-card-actions>
          </v-card>
          <v-card v-if="result" class="elevation-2 mt-3">
            <v-card-title><h1>{{ music.name }}</h1></v-card-title>
            <v-card-text v-html="music.text"></v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
          <v-dialog v-model="dialog" max-width="290">
            <v-card>
              <v-card-title class="headline">{{ titleDialog }}</v-card-title>
              <v-card-text>{{ msgDialog }}</v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="green darken-1" flat="flat" @click.native="dialog = false">Fechar</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
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
        txtartist: '',
        txtmusic: '',
        result: '',
        dialog: false,
        titleDialog: '',
        msgDialog: '',
        music: {
          name: '',
          text: ''
        }
      }
    },
    methods: {
      findMusic () {
        if (this.txtartist && this.txtmusic) {
          axios.get('https://api.vagalume.com.br/search.php?art=' + this.txtartist + '&mus=' + this.txtmusic + '&apikey={bcd3ff0cd991b534b5c2038f183788c2}')
            .then(response => {
              this.result = response.data
              if (this.result.type === 'exact') {
                this.music.name = this.result.mus[0].name
                this.music.text = this.result.mus[0].text.replace(/(?:\r\n|\r|\n)/g, '<br />')
                console.log(this.music)
              }
              if (this.result.type === 'song_notfound' || this.result.type === 'notfound') {
                this.dialog = true
                this.titleDialog = 'Erro'
                this.msgDialog = 'Não foi possível localizar sua música.'
                this.txtmusic = ''
                this.txtartist = ''
              }
            })
            .catch(e => {
              this.dialog = true
              this.titleDialog = 'Erro'
              this.msgDialog = 'Falha ao conectar ao servidor, tente novamente mais tarde.'
              console.log(e)
            })
        } else {
          this.dialog = true
          this.titleDialog = 'Erro'
          this.msgDialog = 'Os campos Artista e Música são obrigatórios.'
        }
      }
    }
  }
</script>

<style scoped>

</style>
