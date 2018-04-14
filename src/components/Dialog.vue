<template>
  <v-dialog v-model="dialog" max-width="290">
    <v-card>
      <v-card-title class="headline">{{ title }}</v-card-title>
      <v-card-text>{{ msg }}</v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="green darken-1" flat="flat" @click="changeDialogo">Fechar</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
    name: 'Dialog',
    props: ['title', 'msg', 'dialog'],
    methods: {
      changeDialogo () {
        this.$emit('dialogo', false)
      }
    }
  }
</script>

<style scoped>

</style>
