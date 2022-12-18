<template>
  <div class="inventory-list">
    <div
      draggable="false"
      :key="index"
      v-for="(_, index) in new Array(25).fill(0)"
      class="inventory-list__item"
      @dragover.prevent
      @dragenter.prevent
      @drop="onDrop($event, index)"
    >
      <InventoryItemContent
        @customClick="inventoryItemClick"
        @dragStart="dragStart"
        :inventoryItem="getInventoryByCellId(index)"
        v-if="getInventoryByCellId(index)"
      ></InventoryItemContent>
    </div>
  </div>
</template>


<script>
import InventoryItemContent from "@/components/InventoryItemContent.vue";

export default {
  props: {
    inventory: {
      type: Array,
      required: true,
    },
  },
  components: { InventoryItemContent },
  

  data: () => {
    return {
      activeDragElementId: 0,
    };
  },

  methods: {
    getInventoryByCellId(cellId) {
      return this.inventory.find(
        (inventoryItem) => inventoryItem.cellId === cellId
      );
    },

    onDrop(_, indexCell){
        this.$emit('updateElementCell', {elementId: this.activeDragElementId, indexCell: indexCell})
    },

    inventoryItemClick(data){
        this.$emit('openModalInfo', data)
    },

    dragStart(data) {
      this.activeDragElementId = data.id;
    },
  },
};
</script>