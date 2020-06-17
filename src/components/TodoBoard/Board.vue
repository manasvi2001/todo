<template>
  <div class="board__container">
    <div class="board__heading">
      {{ boardName }}
    </div>
    <div class="board__content">
      <div class="item__container" v-if="boardName === 'to do'">
        <div
          style="width: 100%; font-weight: bold; font-style: italic;"
          @click="addTask"
          v-if="!addingNewTask"
        >
          Add a new task...
        </div>
        <div v-if="addingNewTask">
          <input
            v-model="newTask"
            ref="newtask"
            @keyup.enter="addNewTask"
            @blur="cancelAddTask"
          />
        </div>
      </div>
      <app-item
        v-for="(item, index) in items"
        :key="item"
        :title="item"
        :index="index"
        :allowEdit="boardName !== 'done'"
      ></app-item>
    </div>
  </div>
</template>

<script>
import Item from "./Item.vue";

export default {
  data() {
    return {
      boardName: this.board,
      boardItems: this.items,
      newTask: "",
      addingNewTask: false
    };
  },
  props: ["board", "items"],
  components: {
    appItem: Item
  },
  methods: {
    cancelAddTask() {
      this.addingNewTask = false;
    },
    addTask() {
      this.addingNewTask = true;
    },
    addNewTask() {
      if (!this.newTask.length) {
        return;
      }
      this.addingNewTask = false;
      this.$parent.addTaskToBoard(this.newTask, this.boardName);
    },
    updateTask(item, index) {
      this.$parent.updateTask(item, this.boardName, index);
    },
    deleteTask(index) {
      this.$parent.deleteTask(this.boardName, index);
    }
  }
};
</script>

<style lang="scss" scoped>
.board {
  &__container {
    width: 100%;
    margin-right: 5rem;
    text-align: left;
  }

  &__heading {
    font-weight: bold;
    font-size: 3rem;
  }

  &__content {
    display: flex;
    flex-direction: column;
  }
}
</style>
