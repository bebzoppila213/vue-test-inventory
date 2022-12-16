<template>
  <div class="inventory-sidebar">
    <img class="inventory-sidebar__img" src="@/assets/cat.png" alt="" />
    <h2 class="inventory-sidebar__title">Тайтл</h2>
    <h3 class="inventory-sidebar__subtitle">Сабтайтл</h3>
  </div>
</template>


<style>

.inventory-sidebar {
  flex: 1 1 15%;
  padding: 15px;
  display: flex;
  align-items: center;
  flex-direction: column;
  border: 1px solid #4d4d4d;
  justify-content: flex-start;
  background-color: #4d4d4d;
  border-radius: 20px;
}
.inventory-sidebar__title {
  margin-top: 10px;
}

.inventory-sidebar__img {
  max-width: 200px;
}
</style>