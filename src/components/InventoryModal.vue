<template>
  <div class="inventory-modal">
    <button @click="$emit('closeModal')" class="inventory-modal__close">
      X
    </button>
    <img class="inventory-modal__img" :src="inventoryItem.img" alt="" />
    <div class="inventory-modal__title">Название {{ inventoryItem.name }}</div>
    <ul class="inventory-modal__characteristic">
      <li
        :key="indx"
        v-for="(characteristic, indx) in inventoryItem.characteristics"
        class="inventory-modal__characteristic-item"
      >
        {{ characteristic }}
      </li>
      <li class="inventory-modal__characteristic-item">
        Колличество {{ inventoryItem.count }}
      </li>
    </ul>
    <inventory-menu @changeInventoryItemCount="(data) => $emit('changeInventoryItemCount', data)" :inventoryItem="inventoryItem"></inventory-menu>
    
  </div>
</template>

<script>
import InventoryMenu from "./InventoryMenu.vue";

export default {
  components: {
    InventoryMenu,
  },
  props: {
    inventoryItem: Object,
  },
  data: () => {
    return {
    };
  },

  methods: {

  },
  computed: {
  },
};
</script>


<style>
.inventory-modal__img {
  max-width: 200px;
}

.inventory-modal__close {
  position: absolute;
  top: 10px;
  cursor: pointer;
  right: 10px;
  color: rgb(255, 0, 0);
  font-size: 20px;
  background-color: transparent;
  border: 0px;
}

.inventory-modal {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.inventory-modal__btn {
  width: 100%;
  padding: 7px 0px;
  cursor: pointer;
  background-color: red;
  color: #fff;
  border: 0px;
}

.inventory-modal__menu {
  
}

.inventory-modal__menu-input {
  flex: 1 1 100%;
}

.inventory-modal__menu-btn {
  padding: 8px 10px;
  border-radius: 10px;
  cursor: pointer;
  border: 0px;
  font-weight: bold;
  box-shadow: 0px 0px 27px -3px #fa7272;
}

.inventory-modal__menu-cansel {
  background-color: #fff;
  flex:1 1 40%;
}

.inventory-modal__menu-confirm {
  background-color: #fa7272;
  color: #fff;
  flex:1 1 40%;
}

.inventory-modal__menu-input {
  padding: 10px;
  background-color: #262626;
  border: 1px solid #4d4d4d;
  outline: none;
  color: #fff;
  font-size: 14px;
}

.inventory-modal__menu-input--error {
  border: 1px solid #fa7272;
}
</style>