<template>
  <div class="inventory-black inventory">
    <div class="container">
      <div class="inventory__inner">
        <inventory-sidebar> </inventory-sidebar>
        <inventory-list></inventory-list>
      </div>
    </div>
  </div>
  <div>
  </div>
</template>

<script>
import InventoryList from "./components/InventoryList.vue"
import InventorySidebar from "./components/InventorySidebar.vue"

export default {
  name: "App",
  components: {
    InventoryList,
    InventorySidebar
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


.inventory-list::-webkit-scrollbar {
  display: none;
}
.inventory-list::-webkit-scrollbar-track {
  display: none;
}

</style>