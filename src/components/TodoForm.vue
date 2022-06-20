<script setup lang="ts">
defineProps<{
  addNewTodo: () => void;
  newTodo: string;
}>();
</script>

<template>
  <form @submit.prevent="addNewTodo">
    <input
      placeholder="Add new Todo"
      :value="newTodo"
      @input="
        $emit('update:newTodo', ($event.target as HTMLInputElement)?.value)
      "
      class="input"
      name="newTodo"
    />
    <button class="button">
      Add <font-awesome-icon icon="fa-solid fa-plus" />
    </button>
  </form>
</template>

<style scoped>
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
