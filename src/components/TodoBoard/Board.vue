<template>
  <div class="board__container">
    <div class="board__heading">
      {{ boardName }}
    </div>
    <div class="board__content">
      <div
        class="item__container"
        @click="addTask"
        v-if="boardName === 'to do'"
      >
        Add a new task
      </div>
      <div class="item__container" v-if="addingNewTask">
        <input v-model="newTask" @blur="addNewTask" />
      </div>
      <app-item
        v-for="(item, index) in items"
        :key="index"
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
    addTask() {
      this.addingNewTask = true;
    },
    addNewTask() {
      this.addingNewTask = false;
      this.$parent.addTaskToBoard(this.newTask, this.boardName);
    },
    updateTask(item, index) {
      console.log(item, index);
      this.$parent.updateTask(item, this.boardName, index);
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
    // border: 1px solid red;
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
