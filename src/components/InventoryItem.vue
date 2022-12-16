<template>
  <div
    @click="onClick"
    draggable="true"
    @dragstart="onDragStart"
    class="inventory-list__item-inner"
  >
    <img draggable="false" :src="inventoryItem.img" alt="" />
    <div class="inventory-list__item-number">{{ inventoryItem.count }}</div>
  </div>
</template>

<script>

export default {
  props: {
    inventoryItem: Object,
  },
  methods: {
    onDragStart(event) {
      this.changeClassDragElement(event);
      event.dataTransfer.dropEffect = "move";
      event.dataTransfer.effectAllowed = "move";
      this.$emit("customDragStart", { id: this.inventoryItem.id });
    },

    changeClassDragElement(event) {
      event.target.classList.add("inventory-list__item-inner--dragable");
      setTimeout(() => {
        event.target.classList.remove("inventory-list__item-inner--dragable");
      }, 0);
    },

    onClick() {
      this.$emit("customClick", { id: this.inventoryItem.id });
    },
  },
};
</script>

<style>
.inventory-list__item-number {
  position: absolute;
  bottom: 0px;
  right: 0px;
  padding: 4px;
}

.inventory-list__item-img {
  width: 100%;
  height: 100%;
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
.inventory-list__item-inner--dragable {
  border-radius: 20px;
  border: 3px solid #4d4d4d;
  background-color: #262626;
  box-shadow: 0px 5px 61px -3px rgba(0, 0, 0, 0.1);
}
</style>