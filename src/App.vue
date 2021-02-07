<template>
  <v-app>
    <v-app-bar app color="primary" flat>
      <v-app-bar-title class="white--text"> VueDraggable Kanban </v-app-bar-title>
    </v-app-bar>

    <v-main>
      <Board />
    </v-main>
  </v-app>
</template>

<script>
import Board from './components/Board'

export default {
  components: {
    Board,
  }
}
</script>
