<template>
  <div class="inventory-list">
    <inventory-modal
      @closeModal="closeElement()"
      :inventoryItem="inventory.find((itm) => itm.id === activeModalItemId)"
      v-if="elementIsOpen"
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
        :inventoryItem="getItemByСellId(indx)"
        @customClick="openInventoryModal"
        @customDragStart="onDragStart"
        v-if="getItemByСellId(indx)"
      />
    </div>
  </div>
</template>

<script>
import InventoryItem from "./InventoryItem.vue";
import { defaultState } from "../default/DefaultInventoryState";
import InventoryModal from "./InventoryModal.vue";
import OpenCloseElementMixin from "../mixins/OpenCloseElementMixin.vue"

export default {
  name: "InventoryList",
  components: {
    InventoryItem,
    InventoryModal,
  },
  mixins: [OpenCloseElementMixin],

  created() {
    const data = localStorage.getItem("InventoryList");
    if (data) {
      this.inventory = JSON.parse(data);
    }
  },

  data: () => {
    return {
      inventory: defaultState,
      activeDrugId: 0,
      activeModalItemId: 0,
    };
  },

  methods: {
    changeInventoryItemCount(data) {
      const inventoryItem = this.inventory.find((itm) => itm.id === data.id);
      if(!inventoryItem) return null
      inventoryItem.count = Math.max(0, inventoryItem.count - data.value);
      if (inventoryItem.count === 0) {
        this.openElement()
        this.inventoryItem = this.inventory.filter((fItem) => fItem.id !== inventoryItem.id);
      }
    },

    openInventoryModal(data) {
      this.activeModalItemId = data.id;
      this.openElement()
    },

    getItemByСellId(cellId) {
      const item = this.inventory.find((itm) => itm.cellId === cellId);
      if (item) {
        return item;
      }
      return null;
    },

    onDragStart(idItem) {
      this.activeDrugId = idItem.id;
    },

    onDrop(_, cellId) {
      const inventoryItem = this.inventory.find((itm) => itm.id === this.activeDrugId);
      if (inventoryItem) {
        inventoryItem.cellId = cellId;
      }
    },
  },

  watch: {
    inventory: {
      handler: function (val) {
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