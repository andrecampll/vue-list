<script setup lang="ts">
import TodoItem from "@/components/TodoItem.vue";

type Todo = { id: number; done: boolean; content: string };

defineProps<{
  todos: Todo[];
  toggleDone: (todo: Todo) => void;
  removeTodo: (index: number) => void;
  removeAll: () => void;
  markAllDone: () => void;
  createdTasks: number;
  doneTasks: number;
}>();
</script>

<template>
  <div class="todo-list-body">
    <header class="todo-list-header">
      <h2 class="created-tasks">Created tasks {{ createdTasks }}</h2>
      <h2 class="finished-tasks">Finished {{ doneTasks }}</h2>
    </header>
    <ul>
      <li
        @click="toggleDone(todo)"
        v-for="(todo, index) in todos"
        :key="todo.id"
      >
        <TodoItem
          :onRemoveTodo="() => removeTodo(index)"
          :done="todo.done"
          :content="todo.content"
        />
      </li>
    </ul>

    <footer>
      <button @click="markAllDone" class="button mark-all">
        Mark all done
      </button>
      <button @click="removeAll" class="button remove-all">Remove all</button>
    </footer>
  </div>
</template>

<style scoped>
footer {
  display: flex;
  align-items: center;
  margin-top: 16px;
}

.button {
  background: var(--purple);
  border: 0;
  border-radius: 8px;
  width: 120px;
  height: 42px;
  color: #fff;
  font-weight: bold;
  font-size: 0.9rem;
  cursor: pointer;
  margin-right: 8px;
  margin-left: 0;
}

.mark-all {
  background: var(--blue);
}

.todo-list-body {
  width: 100%;
  max-width: 736px;
}

.todo-list-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.created-tasks {
  color: var(--blue);
  font-weight: bold;
  font-size: 0.875rem;
}

.finished-tasks {
  color: var(--purple);
  font-weight: bold;
  font-size: 0.875rem;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 12px;
}
</style>
