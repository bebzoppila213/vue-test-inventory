<template>
  <section class="inventory">
    <div class="container">
      <div class="inventory__inner">
        <div class="inventory-main">
          <InventorySidebar></InventorySidebar>
          <InventoryList
            @openModalInfo="openModalInfo"
            @updateElementCell="updateElementCell"
            :inventory="inventory"
          ></InventoryList>
          <InventoryModal
            @closeModal="closeModal()"
            v-if="modalIsOpen"
            :inventoryItem="modalInventoryData"
            @changeInventoryItemCount="changeInventoryItemCount"
          ></InventoryModal>
        </div>
        <div class="inventory-search">
          <button class="inventory-search__btn"></button>
          <input class="inventory-search__input" type="text" />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import InventoryList from "@/components/InventoryList.vue";
import InventorySidebar from "@/components/InventorySidebar.vue";
import InventoryModal from "@/components/InventoryModal.vue";
import { defaultState } from "@/default/DefaultInventory";
import ModalMixin from "@/mixins/ModalMixin.vue";
export default {
  components: { InventoryList, InventorySidebar, InventoryModal },
  mixins: [ModalMixin],

  created() {
    const inventory = localStorage.getItem("inventory");
    if (inventory) {
      this.inventory = JSON.parse(inventory);
    }
    this.setSelector(".inventory-modal");
  },

  data: () => {
    return {
      inventory: defaultState,
      modalInventoryData: null,
    };
  },

  methods: {
    findInventoryItemById(elementId) {
      return this.inventory.find((inventoryI) => inventoryI.id === elementId);
    },

    updateElementCell({ elementId, indexCell }) {
      const inventoryItem = this.findInventoryItemById(elementId);
      if (!inventoryItem) return null;
      inventoryItem.cellId = indexCell;
    },

    openModalInfo({ id }) {
      this.modalInventoryData = this.findInventoryItemById(id);
      this.openModal();
    },

    changeInventoryItemCount({ id, count }) {
      const inventoryItem = this.findInventoryItemById(id);
      inventoryItem.count = Math.max(0, inventoryItem.count - count);
      this.inventory = this.inventory.filter(
        (inventoryItem) => inventoryItem.count > 0
      );
    },
  },

  watch: {
    inventory: {
      handler(val) {
        localStorage.setItem("inventory", JSON.stringify(val));
      },
      deep: true,
    },
  },
};
</script>

<style>
@import url(./assets/style/style.css);
</style>
