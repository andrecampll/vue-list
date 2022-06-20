<template>
  <div class="empty-content">
    <img src="../assets/clipboard.svg" />

    <div class="empty-tips">
      <h2>You don't have any todos yet</h2>
      <span>Create and organize your todos 😁</span>
    </div>
  </div>
</template>

<style scoped>
.empty-content {
  display: flex;
  align-items: center;
  flex-direction: column;

  padding: 64px;
  border-top: 1px solid var(--gray-400);
  margin-top: 24px;
}

.empty-tips {
  display: flex;
  flex-direction: column;
  align-items: center;

  margin-top: 16px;
}

h2,
span {
  font-size: 1rem;
  color: var(--gray-300);
}

h2 {
  font-weight: bold;
}
</style>
