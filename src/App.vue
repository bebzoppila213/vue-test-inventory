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
            :inventoryItem="modalData"
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
import localStorageMixin from "@/mixins/LocalStorageMixin.vue"

export default {
  components: { InventoryList, InventorySidebar, InventoryModal },
  mixins: [ModalMixin, localStorageMixin],

  created() {
    this.setModalSelector(".inventory-modal");
    this.setLocalStorageField('inventory')
  },

  data: () => {
    return {
      inventory: defaultState,
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
      this.modalData = this.findInventoryItemById(id);
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
};
</script>

<style>
@import url(./assets/style/style.css);
</style>
