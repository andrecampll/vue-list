<script setup lang="ts">
import { ref, onMounted } from "vue";
import TodoItem from "@/components/TodoItem.vue";

type Todo = { id: number; done: boolean; content: string };

const todos = ref<Todo[]>([]);
const newTodo = ref("");

const addNewTodo = () => {
  todos.value.push({
    id: Date.now(),
    done: false,
    content: newTodo.value,
  });

  newTodo.value = "";
};

const toggleDone = (todo: Todo) => {
  todo.done = !todo.done;
};

const removeTodo = (index: number) => todos.value.splice(index, 1);

const markAllDone = () => todos.value.forEach((todo) => (todo.done = true));

const removeAll = () => (todos.value = []);

onMounted(() => {
  console.log(`The initial todos is ${todos.value}`);
});
</script>

<template>
  <header class="header">
    <img src="./assets/todo.svg" alt="" />
  </header>

  <main>
    <div class="content">
      <form @submit.prevent="addNewTodo">
        <input
          placeholder="Add new Todo"
          v-model="newTodo"
          class="input"
          name="newTodo"
        />
        <button class="button">Criar</button>
      </form>

      <div class="todo-list-body">
        <header class="todo-list-header">
          <h2 class="created-tasks">Created tasks</h2>
          <h2 class="finished-tasks">Finished</h2>
        </header>
        <ul>
          <li
            @click="toggleDone(todo)"
            v-for="(todo, index) in todos"
            :key="todo.id"
            class="todo"
            :class="{ todoDone: todo.done }"
          >
            <TodoItem
              :onRemoveTodo="() => removeTodo(index)"
              :done="todo.done"
              :content="todo.content"
            />
          </li>
        </ul>
        <button @click="removeAll">Remove all</button>
        <button @click="markAllDone">Mark all done</button>
      </div>
    </div>
  </main>
</template>

<style>
@import "./assets/base.css";

#app {
  font-weight: normal;
  height: 100%;
}

.header {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  padding: 72px;
  height: 20%;
}

main {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;

  flex-direction: column;
  width: 100%;
  background: var(--vt-c-black-soft);
  transition: color 0.5s, background-color 0.5s;
  height: 80%;
}

.content {
  margin: 0 auto;
  width: 100%;
  height: 100%;
  max-width: 736px;
}

form {
  display: flex;
  align-items: center;
  width: 100%;
  height: 54px;
  position: relative;
  bottom: 30px;
}

.button {
  background: var(--blue-button);
  border: 0;
  border-radius: 8px;
  width: 90px;
  height: 52px;
  color: #fff;
  font-weight: bold;
  font-size: 1rem;
  cursor: pointer;
  margin-left: 8px;
}

.input {
  background: #262626;
  border: 0;
  width: 100%;
  height: 100%;
  max-width: 638px;
  border-radius: 8px;
  padding: 16px;
  font-size: 1rem;
  color: var(--white);
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
