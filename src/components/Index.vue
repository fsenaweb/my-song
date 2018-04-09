<template>

  <v-content>
    <v-container fluid fill-height>
      <v-layout align-center justify-center>
        <v-flex xs12 sm8 md4>
          <v-card class="elevation-12">
            <v-card-title primary-title>
              <div class="headline">Repertório Musical</div>
              <div>Pesquise pela letras das canções e curta com seus amigos nos melhores momentos de lazer.</div>
            </v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn :to="'home'" depressed small color="primary">Comece agora</v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </v-content>

</template>

<script>
  export default {
    name: 'Index'
  }
</script>

<style scoped>

</style>
