<template>
  <div class="inventory-modal__menu">
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
</template>

<script>
export default {
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
        this.$emit("changeInventoryItemCount", {
          id: this.inventoryItem.id,
          value: Number(this.inputState),
        });
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