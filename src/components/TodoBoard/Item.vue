<template>
  <div
    class="item__container"
    :class="{ item__done: !allowEditOption }"
    draggable="true"
    @dragstart="handleDragStart($event)"
  >
    <div class="item__title" v-if="!editing">
      {{ title }}
    </div>
    <div class="item__title" v-else>
      <input v-model="updatedTask" @keyup.enter="updateTask(index)" />
    </div>
    <div class="item__edit" v-if="allowEditOption">
      <div class="item__edit--icon" @click.prevent="editTask">e</div>
      <div class="item__edit--icon" @click.prevent="deleteTask">d</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      allowEditOption: this.allowEdit,
      updatedTask: this.title,
      editing: false
    };
  },
  props: ["title", "allowEdit", "index", "board"],
  methods: {
    editTask() {
      this.editing = true;
    },
    updateTask() {
      this.editing = false;
      this.$parent.updateTask(this.updatedTask, this.index);
    },
    deleteTask() {
      // Call parent method
      this.$parent.deleteTask(this.index);
    },
    handleDragStart(e) {
      e.dataTransfer.dropEffect = "move";
      e.dataTransfer.effectAllowed = "move";
      e.dataTransfer.setData(
        "draggedItem",
        JSON.stringify({
          title: this.title,
          board: this.board,
          index: this.index
        })
      );
    }
  }
};
</script>

<style lang="scss">
.item {
  &__container {
    margin: 1rem 0;
    box-shadow: 2px 2px 5px lighten(#000000, 60%);
    padding: 1rem;
    border-radius: 5px;
    cursor: pointer;
    display: flex;
    flex-direction: row;
    justify-content: space-between;

    &[draggable] {
      -moz-user-select: none;
      -khtml-user-select: none;
      -webkit-user-select: none;
      user-select: none;
    }
  }

  &__done {
    background-color: lighten(green, 20%);
  }

  &__edit {
    display: flex;
    justify-content: space-between;

    &--icon {
      margin: 0 0.5rem;
    }
  }
}
</style>
