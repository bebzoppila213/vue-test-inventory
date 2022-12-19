
<script>
export default {
  mounted() {
    document.addEventListener("click", this.documentClick);
  },

  data: () => {
    return {
      modalIsOpen: false,
      modalSelector: "",
      flag: false,
      modalData: null,
    };
  },

  methods: {
    openModal() {
      this.modalIsOpen = true;
    },

    closeModal() {
      console.log("close");
      this.modalIsOpen = false;
    },

    setModalData(newModalData){
        this.modalData = newModalData
    },

    setSelector(newSelector) {
      this.selector = newSelector;
    },

    documentClick(event) {
      const element = document.querySelector(this.selector);
      if (this.flag) {
        if (!event.composedPath().includes(element)) {
          this.modalIsOpen = false;
          this.flag = false;
        }

        return;
      }
      this.flag = true;
    },
  },
};
</script>