<script setup lang="ts">
defineProps<{
  done: boolean;
  content: string;
  onRemoveTodo: () => void;
}>();
</script>

<template>
  <div class="todo" :class="{ todoDone: done }">
    <div class="todo-content">
      <input type="radio" class="todo-radio" :checked="done" />
      <p :class="{ done }">
        {{ content }}
      </p>
    </div>
    <button @click="onRemoveTodo" class="delete-button">
      <font-awesome-icon
        icon="fa-regular fa-trash-can"
        size="lg"
        :style="{ color: '#808080' }"
      />
    </button>
  </div>
</template>

<style scoped>
.todo {
  cursor: pointer;
  display: flex;
  width: 100%;
  justify-content: space-between;
  background: var(--gray-500);
  padding: 16px;
  font-size: 1rem;
  color: var(--white);
  border-radius: 8px;
  border: 1px solid var(--gray-400);
  margin-top: 12px;
  transition: opacity 0.3s ease;
}

.todo-content {
  display: flex;
  align-items: center;
}

.done {
  text-decoration: line-through;
  transition: all 0.3s ease;
}

.todo-radio {
  appearance: none;
  margin: 0;
  background-color: var(--gray-500);
  font: inherit;
  color: var(--blue);
  width: 1.15em;
  height: 1.15em;
  border: 0.15em solid var(--blue);
  border-radius: 50%;
  display: grid;
  place-content: center;
  cursor: pointer;
  margin-right: 12px;
  transition: all 0.3s ease;
}

.todo-radio:checked {
  background-color: var(--purple);
  border: 0.15em solid var(--purple);
}

.todoDone {
  opacity: 0.7;
}

.delete-button {
  background: none;
  border: 0;
  cursor: pointer;
}
</style>
