<template>
  <div class="inventory-modal">
    <button @click="$emit('closeModal')" class="inventory-modal-close">
      &times;
    </button>
    <div class="inventory-modal-content">
      <img
        class="inventory-modal-content__img"
        :src="inventoryItem.img"
        alt="Картинка"
      />
      <hr class="inventory-modal-hr" />
      <h3 class="inventory-modal-content__title">{{ inventoryItem.name }}</h3>
      <h4 class="inventory-modal-content__count">
        Колличество:{{ inventoryItem.count }}
      </h4>
      <ul>
        <li
          :key="characteristics"
          v-for="characteristics in inventoryItem.characteristics"
        >
          {{ characteristics }}
        </li>
      </ul>
    </div>
    <div v-if="menuIsOpen" class="inventory-modal-menu">
      <input
        v-model="inputState"
        class="inventory-modal-menu__input"
        type="text"
      />
      <button
        @click="menuIsOpen = false"
        class="inventory-modal-menu__cancel inventory-modal-menu__btn"
      >
        Отмена
      </button>
      <button
        @click="sendForm"
        class="inventory-modal-menu__send inventory-modal-menu__btn"
      >
        Подтвердить
      </button>
    </div>
    <button
      @click="menuIsOpen = true"
      v-if="!menuIsOpen"
      class="inventory-modal__btn"
    >
      Удалить предмет
    </button>
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

  data: () => {
    return {
      menuIsOpen: false,
      inputState: "",
    };
  },

  methods: {
    sendForm() {
      if (/^\d+$/.test(this.inputState)) {
        this.$emit("changeInventoryItemCount", {
          count: Number(this.inputState),
          id: this.inventoryItem.id,
        });
        this.inputState = ''
        this.menuIsOpen = false
      }
    },
  },
};
</script>