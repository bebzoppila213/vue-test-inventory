<template>
  <div  class="inventory-modal__menu">
    <div class="inventory-modal__menu-form" v-if="elementIsOpen">
      <input v-model="inputState" :class="getInputClass" type="text" />
      <button
        @click="closeElement()"
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
        v-if="!elementIsOpen"
        @click="openElement()"
        class="inventory-modal__btn"
      >
        Удалить предмет
      </button>
    </div>
  </div>
</template>

<script>

import OpenCloseElementMixin from "../mixins/OpenCloseElementMixin.vue"

export default {
  props:{
    inventoryItem: Object,
  },
  mixins:[OpenCloseElementMixin],
  data: () => {
    return {
      inputState: "",
      errors: false,
    };
  },

  methods: {
    onClickBtnConfirm() {
      const regNumber = /^\d+$/;
      if (regNumber.test(this.inputState)) {
        this.validNumber();
      } else {
        this.errors = true;
      }
    },

    validNumber(){
      this.$emit("changeInventoryItemCount", {id: this.inventoryItem.id,value: Number(this.inputState),});
        this.closeElement();
        this.errors = false;
        this.inputState = ''
    }
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