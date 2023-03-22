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
@import "@/assets/scss/config/mixin.scss";
.wrapper {
  position: relative;
  right: 3rem;
  margin-bottom: 1.5rem;
  width: 20rem;
  padding: 0.5rem;
  min-height: 4rem;
  display: flex;
  justify-content: space-around;
  box-shadow: 0px 2px 8px rgba(72, 72, 72, 0.25);
  border-radius: 4px;

  @include mq("desktop") {
    width: 30rem;
    min-height: 5rem;
  }

  &.-dark {
    background-color: #242424;
    color: #fff;
  }
  .notification {
    display: flex;
    align-items: center;

    &__title {
      margin-left: 1rem;
      font-family: "Inter", sans-serif;
      font-weight: 500;
      font-size: 1.2rem;
      line-height: 1.4rem;

      @include mq("desktop") {
        font-size: 1.8rem;
        line-height: 2.2rem;
      }
    }

    &__icon {
      width: 2rem;
      height: 2rem;
      flex-shrink: 0;
      order: -1;
      background-repeat: no-repeat;
      background-size: 2rem;

      @include mq("desktop") {
        width: 2.4rem;
        width: 2.4rem;
        height: 2.4rem;
      }

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
    width: 3.2rem;
    height: 3.2rem;
    align-self: center;
    cursor: pointer;
    background-color: transparent;

    &__icon {
      width: 2rem;

      @include mq("desktop") {
        width: 2.4rem;
      }
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
