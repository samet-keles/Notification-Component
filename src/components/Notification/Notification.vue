<script setup>
import { ref } from "vue";

const props = defineProps(["type", "title", "theme"]);

const hidden = ref(true);

function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

delay(7500).then(() => (hidden.value = false));
</script>

<template>
  <Transition name="slide-fade">
    <div
      class="wrapper"
      :class="{ '-dark': props.theme == 'dark' }"
      v-if="hidden"
    >
      <div class="notification">
        <h3 class="notification__title">{{ props.title }}</h3>
        <div class="notification__icon" :class="props.type"></div>
      </div>
      <button class="button" @click="hidden = !hidden">
        <img
          class="button__icon"
          src="@/assets/img/icon/close.svg"
          alt="close"
        />
      </button>
    </div>
  </Transition>
</template>

<style lang="scss" scoped>
.wrapper {
  position: relative;
  right: 30px;
  margin-bottom: 15px;
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

      &.success {
        background-image: url("@/assets/img/icon/success.svg");
      }

      &.info {
        background-image: url("@/assets/img/icon/info.svg");
      }

      &.warning {
        background-image: url("@/assets/img/icon/warning.svg");
      }

      &.danger {
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
.slide-fade {
  &-enter {
    &-active {
      transition: all 0.3s ease-out;
    }
  }

  &-leave {
    &-active {
      transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
    }
    &-to {
      transform: translateX(20px);
      opacity: 0;
    }
  }
}
</style>
