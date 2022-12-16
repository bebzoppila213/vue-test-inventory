<template>
  <div class="inventory-black inventory">
    <div class="container">
      <div class="inventory__inner">
        <div class="inventory-sidebar">
          <img class="inventory-sidebar__img" src="./assets/cat.png" alt="" />
          <h2 class="inventory-sidebar__title">Тайтл</h2>
          <h3 class="inventory-sidebar__subtitle">Сабтайтл</h3>
        </div>
        <inventory-list></inventory-list>
      </div>
    </div>
  </div>
  <div>
  </div>
</template>

<script>
import InventoryList from "./components/InventoryList.vue"
export default {
  name: "App",
  components: {
    InventoryList
  },

  data: () => {
    return {

    };
  },

  methods: {

  },
};
</script>

<style>
@import url("./assets/fonts/stylesheet.css");
body{
  background-color: #1E1E1E;
}
* {
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}
img {
  max-width: 100%;
}
.container {
  max-width: 1100px;
  margin: 0 auto;
}
.inventory__inner {
  display: flex;
  position: relative;
  gap: 30px;
  height: 470px;
  /*  */
  color: #fff;
}
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
.inventory-list {
  flex: 1 1 70%;
  background-color: #4d4d4d;
  border-radius: 20px;
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  overflow: auto;
}
.inventory-list__item {
  border: 1px solid rgba(255, 255, 255, 0.3);
  z-index: 2;
  aspect-ratio: 1/ 1;
}

.inventory-sidebar__img {
  max-width: 200px;
}

.inventory-list::-webkit-scrollbar {
  display: none;
}
.inventory-list::-webkit-scrollbar-track {
  display: none;
}
.inventory-list__item-inner {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  cursor: grab;
}
.inventory-list__item-inner--dragable{
  border-radius: 20px;
  border: 3px solid #4D4D4D;
  background-color: #262626;
  box-shadow: 0px 5px 61px -3px rgba(0,0,0,0.1);
}
</style>