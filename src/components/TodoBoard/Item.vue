<template>
  <div class="item__container" :class="{ item__done: !allowEditOption }">
    <div class="item__title" v-if="!editing">
      {{ title }}
    </div>
    <div class="item__title" v-else>
      <input v-model="updatedTask" @blur="updateTask(index)" />
    </div>
    <div class="item__edit" v-if="allowEditOption">
      <div class="item__edit--icon" @click.prevent="editTask">e</div>
      <div class="item__edit--icon" @click.prevent="deletetask">d</div>
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
  props: ["title", "allowEdit", "index"],
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
    }
  }
};
</script>

<style lang="scss">
.item {
  &__container {
    margin: 2rem 0;
    box-shadow: 2px 2px 5px lighten(#000000, 60%);
    padding: 1rem;
    border-radius: 5px;
    cursor: pointer;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
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
