<script setup>
import { ref } from "vue";
const props = defineProps(["type", "title", "theme"]);

const show = ref(true);

function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

delay(7500).then(() => (show.value = false));
</script>

<template>
  <div class="wrapper" :class="{ '-dark': props.theme == 'dark' }" v-if="show">
    <div class="notification">
      <h3 class="notification__title">{{ title }}</h3>
      <div
        class="notification__icon"
        :class="{
          '-success': props.type == 'success',
          '-info': props.type == 'info',
          '-warning': props.type == 'warning',
          '-danger': props.type == 'danger',
        }"
      ></div>
    </div>
    <button class="button" @click="show = !show">
      <img class="button__icon" src="@/assets/img/icon/close.svg" alt="close" />
    </button>
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  position: absolute;
  right: 50px;
  bottom: 50px;
  width: 275px;
  height: 50px;
  display: flex;
  justify-content: space-around;
  box-shadow: 0px 2px 8px rgba(72, 72, 72, 0.25);
  border-radius: 4px;

  &.-dark {
    background-color: #242424;
    color: #fff;
  }
  .notification {
    display: flex;
    align-items: center;

    &__title {
      margin-left: 10px;
      font-family: "Inter", sans-serif;
      font-weight: 500;
      font-size: 18px;
      line-height: 22px;
    }

    &__icon {
      width: 24px;
      height: 24px;
      order: -1;
      background-repeat: no-repeat;
      background-size: 24px;

      &.-success {
        background-image: url("@/assets/img/icon/success.svg");
      }

      &.-info {
        background-image: url("@/assets/img/icon/info.svg");
      }

      &.-warning {
        background-image: url("@/assets/img/icon/warning.svg");
      }

      &.-danger {
        background-image: url("@/assets/img/icon/danger.svg");
      }
    }
  }

  .button {
    width: 32px;
    height: 32px;
    align-self: center;
    cursor: pointer;
    background-color: transparent;

    &__icon {
      width: 24px;
    }
  }
}
</style>
