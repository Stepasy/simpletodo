<template>
  <div class="v-todo__holder">
    <ul
      class="v-todo__list"
    >
      <li
        v-for="item in filteredItems"
        :key="item.id"
        :class="[
          'v-todo__list-item',
          {'is-done' : item.isDone},
          {'is-checked' : item.isChecked},
        ]"
      >
        <input
          v-model="item.isChecked"
          type="checkbox"
          class="v-todo__list-checkbox"
        >
        <span class="v-todo__list-text">
          {{ item.text }}
        </span>
        <button
          class="v-todo__list-button v-todo__list-button--done"
          @click="toggleItemData(item.id, 'isDone')"
        >
          {{ item.isDone ? 'Marked as done' : 'Mark as done' }}
        </button>
        <button
          class="v-todo__list-button v-todo__list-button--remove"
          @click="toggleItemData(item.id, 'isRemoved')"
        >
          Remove
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
  },

  computed: {
    filteredItems() {
      return this.items.filter((item) => !item.isRemoved);
    },
  },

  methods: {
    toggleItemData(id, prop) {
      this.items[id][prop] = !this.items[id][prop];
    },
  },
};
</script>

<style lang="scss">
  button {
    appearance: none;
    cursor: pointer;
    padding: 5px;
    border: 1px solid rgba(0, 0, 0, .12);
    background-color: #fff;
    transition: opacity .3s ease-out;

    &:hover {
      opacity: .6;
    }

    &:focus {
      outline: none;
    }
  }

  .v-todo {
    $block: &;

    &__holder {
      max-width: 50%;
    }

    &__list {
      padding: 0;
      margin: 0;
      list-style: none;
    }

    &__list-item {
      display: flex;
      justify-content: space-between;
      padding: 10px;
      border: 1px solid rgba(0, 0, 0, .12);

      &.is-done {
        background-color: #c8f7c8;

        #{$block}__list-text {
          text-decoration: line-through;
        }

        #{$block}__list-button--done {
          background-color: #c8f7c8;
        }
      }

      &.is-checked {
        background-color: #f5f5f5;
      }
    }

    &__list-checkbox {
      margin-right: 10px;
    }

    &__list-text {
      flex-grow: 1;
      display: block;
      margin-right: 10px;
    }

    &__list-button {
      &--done {
        margin-right: 10px;
      }

      &--remove {
        transition: background-color .3s ease-out,
          color .3s ease-out;

        &:hover {
          color: #fff;
          background-color: #ff2d71;
        }
      }
    }
  }
</style>
