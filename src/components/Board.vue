<template>
  <v-container fluid>
    <v-row>
      <v-col class="text-right">
        <v-btn color="primary" depressed @click="addCard"> Add Card </v-btn>
      </v-col>
    </v-row>
    <draggable :list="cards" group="cards" class="row">
      <v-col v-for="(card, i) in cards" :key="i" cols="12" sm="6" md="4">
        <v-card outlined>
          <v-card-title>
            <v-text-field v-model="card.title"></v-text-field>
          </v-card-title>

          <v-spacer></v-spacer>

          <v-card-text>
            <draggable :list="card.tasks" group="tasks" class="row">
              <v-col v-for="(task, j) in card.tasks" :key="j" cols="12">
                <v-text-field v-model="task.title">
                  <template v-slot:append>
                    <v-btn color="error" text class="ml-3" @click="deleteTask(i, j)"> Delete </v-btn>
                  </template>
                </v-text-field>
              </v-col>

              <template v-slot:footer>
                <v-col cols="12">
                  <v-btn color="primary" depressed block @click="addTask(card)"> Add Activity </v-btn>
                </v-col>
                <v-col cols="12">
                  <v-btn color="error" text block @click="deleteCard(i)"> Delete Card </v-btn>
                </v-col>
              </template>
            </draggable>
          </v-card-text>
        </v-card>
      </v-col>
    </draggable>
  </v-container>
</template>

<script>
import Draggable from 'vuedraggable'

export default {
  components: {
    Draggable,
  },
  data: () => ({
    cards: []
  }),  
  methods: {
    addCard() {
      const card = {
        title: 'New Card',
        tasks: [],
      }

      this.cards.push(card)
    },
    deleteCard(index) {
      this.cards = [...this.cards.slice(0, index), ...this.cards.slice(index + 1)]
    },
    addTask(card) {
      const task = {
        title: 'New Activity'
      }

      card.tasks.push(task)
    },
    deleteTask(cardIndex, taskIndex) {
      const card = this.cards[cardIndex]
      card.tasks = [...card.tasks.slice(0, taskIndex), ...card.tasks.slice(taskIndex + 1)]
    }
  }
}
</script>
