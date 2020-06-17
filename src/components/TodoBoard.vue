<template>
  <div class="todoboard__container">
    <app-board
      v-for="(board, index) in boards"
      :key="index"
      :board="board.title"
      :items="board.items"
    ></app-board>
  </div>
</template>

<script>
import Vue from "vue";
import Board from "./TodoBoard/Board.vue";

export default {
  data() {
    return {
      boards: [
        {
          title: "to do",
          items: ["Send the mail", "Check Design options", "Finish the UX flow"]
        },
        {
          title: "doing",
          items: ["Todo feature"]
        },
        {
          title: "done",
          items: ["Add css"]
        }
      ]
    };
  },
  components: {
    appBoard: Board
  },
  methods: {
    addTaskToBoard(item, board) {
      this.boards = this.boards.map(el => {
        if (el.title === board) {
          el.items.push(item);
        }
        return el;
      });
    },
    updateTask(item, board, index) {
      this.boards = this.boards.map(el => {
        if (el.title === board) {
          Vue.set(el.items, index, item);
        }
        return el;
      });
    },
    deleteTask(board, index) {
      this.boards = this.boards.map(el => {
        if (el.title === board) {
          el.items.splice(index, 1);
        }
        return el;
      });
    },
    dropContent(ob) {
      if (ob.board === ob.toBoard) {
        return;
      }
      this.boards = this.boards.map(el => {
        if (el.title === ob.toBoard) {
          el.items.push(ob.title);
        }
        if (el.title === ob.board) {
          el.items.splice(ob.index, 1);
        }
        return el;
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.todoboard {
  &__container {
    display: flex;
    justify-content: space-between;
    max-width: 90%;
  }
}
</style>
