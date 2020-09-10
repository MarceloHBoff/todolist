<template>
  <div class="todo-item">
    <div class="list-item" @dblclick="editTodo">
      <input type="checkbox" v-model="completed" @change="doneEdit" />

      <div
        class="list-label"
        :class="{ completedTodo: completed }"
        v-if="!editing"
      >
        {{ title }}
      </div>

      <input
        type="text"
        class="list-input"
        v-else
        v-model="title"
        v-focus
        @blur="doneEdit"
        @keyup.enter="doneEdit"
        @keyup.esc="cancelEdit"
      />
    </div>

    <button type="button" @click="removeTodo">&times;</button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

interface Todo {
  id: number;
  title: string;
  completed: boolean;
  editing: boolean;
}

export default Vue.extend({
  name: "todo-item",
  props: {
    todo: { type: Object as () => Todo, required: true },
    index: { type: Number, required: true }
  },
  data() {
    return {
      id: this.todo.id,
      title: this.todo.title,
      completed: this.todo.completed,
      editing: this.todo.editing,
      beforeEditCache: ""
    };
  },
  directives: {
    focus: {
      inserted: function(el) {
        el.focus();
      }
    }
  },
  methods: {
    editTodo(): void {
      this.beforeEditCache = this.title;
      this.editing = true;
    },

    cancelEdit(): void {
      this.title = this.beforeEditCache;
      this.editing = false;
    },

    doneEdit(): void {
      if (this.title.trim().length === 0) this.title = this.beforeEditCache;
      this.editing = false;
      this.$emit("finishedEdit", {
        index: this.index,
        todo: {
          id: this.id,
          title: this.title,
          completed: this.completed,
          editing: this.editing
        }
      });
    },

    removeTodo(index: number): void {
      this.$emit("removeTodo", index);
    }
  }
});
</script>

<style scoped lang="scss">
button {
  color: #fff;
  font-size: 26px;
  margin-left: 16px;
}

.list-item {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
}

.list-label {
  width: 100%;
  height: 100%;
  text-align: left;
  padding: 8px 16px;
  line-height: 24px;
  font-size: 18px;
  color: #fff;
  border: 1px solid transparent;
  border-radius: 8px;
  margin-left: 8px;

  &:hover {
    background: #35495e;
  }
}

.list-input {
  width: 100%;
  height: 100%;
  padding: 8px 16px;
  line-height: 24px;
  font-size: 18px;
  color: #fff;
  border: 1px solid #fff;
  border-radius: 8px;
  margin-left: 8px;

  &:focus {
    outline: none;
  }
}

.completedTodo {
  text-decoration: line-through;
  color: #666;
}
</style>
