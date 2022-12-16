<template>
  <div class="inventory-list">
    <inventory-modal
      @closeModal="modalIsOpen = false"
      :inventoryItem="items.find((itm) => itm.id === activeItemId)"
      v-if="modalIsOpen"
      @changeInventoryItemCount="changeInventoryItemCount"
    ></inventory-modal>
    <div
      @dragover.prevent
      @dragenter.prevent
      @drop="onDrop($event, indx)"
      :key="indx"
      v-for="(arrItem, indx) in new Array(30).fill(0)"
      class="inventory-list__item"
    >
      <inventory-item
        @customClick="updateActiveModalItemId"
        @customDragStart="onDragStart"
        :img="getItemByCheckeredId(indx).img"
        :id="getItemByCheckeredId(indx).id"
        :count="getItemByCheckeredId(indx).count"
        v-if="getItemByCheckeredId(indx)"
      />
    </div>
  </div>
</template>

<script>
import InventoryItem from "./InventoryItem.vue";
import { defaultState } from "../default/DefaultInventoryState";
import InventoryModal from "./InventoryModal.vue";
export default {
  name: "InventoryList",
  components: {
    InventoryItem,
    InventoryModal,
  },

  created() {
    const data = localStorage.getItem("InventoryList");
    if (data) {
      this.items = JSON.parse(data);
    }
  },

  data: () => {
    return {
      items: defaultState,
      activeDrugId: 0,
      activeModalItemId: null,
      modalIsOpen: false,
    };
  },

  methods: {
    changeInventoryItemCount(data) {
      const item = this.items.find((itm) => itm.id === data.id);
      item.count = Math.max(0, item.count - data.value);
      if (item.count === 0) {
        this.modalIsOpen = false;
        this.items = this.items.filter((fItem) => fItem.id !== item.id);
      }
    },
    updateActiveModalItemId(data) {
      this.activeModalItemId = data.id;
      this.modalIsOpen = true;
    },

    getItemByCheckeredId(checkeredId) {
      const item = this.items.find((itm) => itm.checkeredId === checkeredId);
      if (item) {
        return item;
      }
      return null;
    },

    onDragStart(idItem) {
      this.activeDrugId = idItem.id;
    },

    onDrop(e, categoryId) {
      const item = this.items.find((itm) => itm.id === this.activeDrugId);
      if (item) {
        item.checkeredId = categoryId;
      }
    },
  },

  watch: {
    items: {
      handler: function (val, oldVal) {
        localStorage.setItem("InventoryList", JSON.stringify(val));
      },
      deep: true,
    },
  },
};
</script>

<style>
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
.inventory-list {
  position: relative;
}
.inventory-modal {
  position: absolute;
  bottom: 0px;
  top: 0px;
  right: 0%;
  left: 60%;
  backdrop-filter: blur(8px);
  z-index: 6;
  border-left: 1px solid #4d4d4d;
  background: rgba(38, 38, 38, 0.5);
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 30px;
  overflow: auto;
}
</style>