<script setup lang="ts">
import { ref, onMounted, computed } from "vue";
import Header from "@/components/Header.vue";
import TodoForm from "@/components/TodoForm.vue";
import TodoList from "@/components/TodoList.vue";

type Todo = { id: number; done: boolean; content: string };

const todos = ref<Todo[]>([]);
const newTodo = ref("");

const addNewTodo = () => {
  if (!newTodo.value) return;

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

const markAllDone = () => todos.value.forEach(toggleDone);

const removeAll = () => (todos.value = []);

const doneTasks = computed(() => todos.value.filter((todo) => todo.done));

onMounted(() => {
  console.log(`The initial todos is ${todos.value}`);
});
</script>

<template>
  <Header />

  <main>
    <div class="content">
      <TodoForm :addNewTodo="addNewTodo" v-model:newTodo="newTodo" />

      <TodoList
        :todos="todos"
        :toggleDone="toggleDone"
        :removeTodo="removeTodo"
        :markAllDone="markAllDone"
        :removeAll="removeAll"
        :doneTasks="doneTasks.length"
        :createdTasks="todos.length"
      />
    </div>
  </main>
</template>

<style>
@import "./assets/base.css";

#app {
  font-weight: normal;
  height: 100%;
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
</style>
