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
                ref="artista"
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
              <v-btn depressed small color="info" @click.prevent="reloadData">Limpar</v-btn>
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
          <dialogo v-if="dialog" :dialog="dialog" :title="titleDialog" :msg="msgDialog" @dialogo="changeDialog"></dialogo>
        </v-flex>
      </v-layout>
    </v-container>
  </v-content>
</template>

<script>
  import axios from 'axios'
  import Dialogo from './Dialog'

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
    components: {
      Dialogo
    },
    methods: {
      changeDialog () {
        this.dialog = false
      },
      findMusic () {
        if (this.txtartist && this.txtmusic) {
          axios.get('https://api.vagalume.com.br/search.php?art=' + this.txtartist + '&mus=' + this.txtmusic + '&apikey={bcd3ff0cd991b534b5c2038f183788c2}')
            .then(response => {
              this.result = response.data
              if (this.result.type === 'exact') {
                this.music.name = this.result.mus[0].name
                this.music.text = this.result.mus[0].text
                  .replace(/(?:\r\n|\r|\n)/g, '<br />')
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
      },
      reloadData () {
        this.txtmusic = ''
        this.txtartist = ''
        this.$refs.artista.focus()
      }
    }
  }
</script>

<style scoped>

</style>
