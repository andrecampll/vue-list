<script setup lang="ts">
import { ref, onMounted } from "vue";

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
  <form @submit.prevent="addNewTodo">
    <label for="">New Todo</label>
    <input v-model="newTodo" name="newTodo" />
    <button>Add new Todo</button>
  </form>

  <button @click="removeAll">Remove all</button>
  <button @click="markAllDone">Mark all done</button>

  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
        {{ todo.content }}
      </h3>
      <button @click="removeTodo(index)">Remove todo</button>
    </li>
  </ul>
</template>

<style>
@import "./assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

form {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  margin: 0 auto;
}

.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
