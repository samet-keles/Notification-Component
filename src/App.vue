<script setup>
import { ref } from "vue";

import Notification from "@/components/Notification/Notification.vue";
import {
  BlueNotification,
  GreenNotification,
  RedNotification,
  YellowNotification,
} from "@/components/Notification/icons/icons.js";

const notifications = ref([]);

function addNotification(type, title, theme) {
  notifications.value.push({
    type: type,
    title: title,
    theme: theme,
  });
}
</script>

<template>
  <div class="wrapper">
    <button
      class="button"
      @click="addNotification('info', 'Notification Info', 'dark')"
    >
      <BlueNotification></BlueNotification>
    </button>

    <button
      class="button"
      @click="addNotification('success', 'Notification Success', 'light')"
    >
      <GreenNotification></GreenNotification>
    </button>

    <button
      class="button"
      @click="addNotification('warning', 'Notification Warning', 'dark')"
    >
      <YellowNotification></YellowNotification>
    </button>

    <button
      class="button"
      @click="addNotification('danger', 'Notification Danger', 'light')"
    >
      <RedNotification></RedNotification>
    </button>
  </div>

  <div class="aside">
    <Notification
      v-for="(notification, index) in notifications"
      :key="index"
      :type="notification.type"
      :title="notification.title"
      :theme="notification.theme"
    ></Notification>
  </div>
</template>

<style lang="scss" scoped>
@import "@/assets/scss/config/mixin.scss";
.wrapper {
  .button {
    padding: 1rem;
    border-radius: 12px;
    background-color: transparent;
    cursor: pointer;

    &:nth-child(odd) {
      background-color: #242424;
    }

    @include mq("tablet") {
      padding: 1.5rem;
    }

    @include mq("desktop") {
      padding: 2rem;
    }
  }
}

.aside {
  max-height: 100vh;
  position: absolute;
  right: 0;
  bottom: 0;
}
</style>
