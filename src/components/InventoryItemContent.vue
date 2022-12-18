<template>
  <div
    @click="$emit('customClick', { id: inventoryItem.id })"
    @dragstart="onDragStart"
    draggable="true"
    class="inventory-list__content"
  >
    <img draggable="false" :src="inventoryItem.img" alt="Карточка" />
    <span class="inventory-list__conten-count">{{ inventoryItem.count }}</span>
  </div>
</template>

<script>
export default {
  props: {
    inventoryItem: {
      type: Object,
      required: true,
    },
  },

  methods: {
    onDragStart(event) {
      event.dataTransfer.dropEffect = "move";
      event.dataTransfer.effectAllowed = "move";
      this.$emit("dragStart", { id: this.inventoryItem.id });
    },
  },
};
</script>