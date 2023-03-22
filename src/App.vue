<script setup>
import { ref } from "vue";
import Notification from "@/components/Notification/Notification.vue";

const notifications = ref([]);

function addNotification() {
  notifications.value.unshift({
    type: "success",
    title: "Notification Title",
    theme: "dark",
  });
}
</script>

<template>
  <button @click="addNotification">Add Notification</button>
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

<style scoped>
.aside {
  max-height: 100vh;
  position: absolute;
  right: 0;
  bottom: 0;
}
</style>
