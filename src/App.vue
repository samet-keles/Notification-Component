<script setup>
import Notification from "@/components/Notification/Notification.vue";
</script>

<template>
  <Transition name="slide-fade">
    <Notification
      type="info"
      title="Notification Title"
      theme="dark"
    ></Notification>
  </Transition>
</template>

<style scoped>
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>
