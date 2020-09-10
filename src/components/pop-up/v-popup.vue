<template>
  <div class="popup-wrapper" ref="popup_wrapper">
      <div class="v-popup">
      <div class="v-popup__header">
        <span>{{popupTitle}}</span>
        <span class="icon">
          <i class="material-icons" @click="closePopUp">close</i>
        </span>
      </div>
      <div class="v-popup__content">
        <slot></slot>
      </div>
      <div class="v-popup__footer">
        <button 
            class="submit-button"
            @click="rightBtnAction(); closePopUp()"
        >
            {{rightBtnTitle}}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-popup",
  components: {},
  props: {
    rightBtnTitle: {
      type: String,
      default: "BUY",
    },
    popupTitle: {
      type: String,
      defaulr: "Popup name",
    },
  },
  methods: {
    closePopUp() {
      this.$emit("closePopUp")
    },
    rightBtnAction() {
        this.$emit("rightBtnAction")
    }
  },
  mounted() {
      let self = this
      document.addEventListener('click', function(item) {
          if (item.target === self.$refs['popup_wrapper']) {
              self.closePopUp()
          }
      })
  },
}
</script>

<style lang="scss" scoped>
.popup-wrapper {
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    background: rgba(64,64,64, .4);
}
.v-popup {
  padding: 16px 25px 16px 25px;
  position: fixed;
  top: 50px;
  right: 0;
  left: 0;
  margin: auto;
  width: 400px;
  z-index: 10;
  box-shadow: 0 0 17px 0 #e7e7e7;
  border: 1px solid #e7e7e7;
  background: #fff;
  &__header,
  &__footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    .icon {
        cursor: pointer;
    }
  }
  &__content {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  &__footer {
    justify-content: center;
    margin-top: 20px;
  }
}
</style>