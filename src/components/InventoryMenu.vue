<template>
  <div  class="inventory-modal__menu">
    <div class="inventory-modal__menu-form" v-if="menuIsOpen">
      <input v-model="inputState" :class="getInputClass" type="text" />
      <button
        @click="menuIsOpen = false"
        class="inventory-modal__menu-cansel inventory-modal__menu-btn"
      >
        Отмена
      </button>
      <button
        @click="onClickBtnConfirm"
        class="inventory-modal__menu-confirm inventory-modal__menu-btn"
      >
        Подтвердить
      </button>
    </div>
    <div>
      <button
        v-if="!menuIsOpen"
        @click="menuIsOpen = true"
        class="inventory-modal__btn"
      >
        Удалить предмет
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    inventoryItem: Object,
  },
  data: () => {
    return {
      inputState: "",
      menuIsOpen: false,
      errors: false,
    };
  },

  methods: {
    onClickBtnConfirm() {
      const regNumber = /^\d+$/;
      if (regNumber.test(this.inputState)) {
        this.$emit("changeInventoryItemCount", {id: this.inventoryItem.id,value: Number(this.inputState),});
        this.menuIsOpen = false;
        this.errors = false;
      } else {
        this.errors = true;
      }
    },
  },

  computed: {
    getInputClass() {
      return (
        "inventory-modal__menu-input " +
        (this.errors ? "inventory-modal__menu-input--error" : "")
      );
    },
  },
};
</script>


<style>

.inventory-modal__menu-form{
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  gap: 6px;
}
</style>