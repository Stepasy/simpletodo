<template>
  <div class="v-todo">
    <div
      v-if="numberOfItemsSelected"
      class="v-todo__text"
    >
      You've selected {{ selectedItemsText }}
    </div>
    <input
      v-model="newItemText"
      type="text"
      class="v-todo__input"
      placeholder="Enter something"
      @change="addItemToList"
    >
    <div>
      <v-todo-items
        v-if="isItemsDeleted"
        :items="items"
      />
      <div
        v-else
        class="v-todo__text"
      >
        Add you first action
      </div>
    </div>

  </div>
</template>

<script>
import VTodoItems from './Partitials/VTodoItems.vue';

export default {
  components: {
    VTodoItems,
  },

  data() {
    return {
      items: [
        {
          id: 0,
          isChecked: false,
          text: 'Bla',
          isDone: false,
          isRemoved: false,
        },
        {
          id: 1,
          isChecked: false,
          text: 'Bla2',
          isDone: false,
          isRemoved: false,
        },
      ],
      newItemText: '',
    };
  },

  computed: {
    numberOfItemsSelected() {
      return this.items.filter((item) => item.isChecked && !item.isRemoved).length;
    },

    isItemsDeleted() {
      return this.items.filter((item) => !item.isRemoved).length;
    },

    selectedItemsText() {
      return `${this.numberOfItemsSelected} ${this.numberOfItemsSelected === 1 ? 'item' : 'items'}`;
    },
  },

  methods: {
    addItemToList() {
      this.items.push({
        id: this.items.length,
        isChecked: false,
        text: this.newItemText,
        isDone: false,
        isRemoved: false,
      });

      this.newItemText = '';
    },
  },
};
</script>

<style lang="scss">
  .v-todo {
    $block: &;

    &__text {
      margin-bottom: 15px;
      font-size: 20px;
    }

    &__input {
      padding: 10px;
      margin-bottom: 15px;
    }
  }
</style>
