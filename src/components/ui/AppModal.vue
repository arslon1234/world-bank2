<template>
  <div class="app-modal" :style="{'width': width}" :class="{ 'app-modal-show': modelValue }">
    <AppTransition>
      <div v-if="modelValue" class="app-modal__body">
        <slot></slot>
      </div>
    </AppTransition>
  </div>
  <app-transition>
    <span
      @click="$emit('update:modelValue', false)"
      v-if="modelValue"
      class="app-modal-shadow"
    ></span>
  </app-transition>
</template>
<script setup>
import AppTransition from "@/components/ui/AppTransition";
const props = defineProps({
  modelValue: {
    type: Boolean,
    default: false,
  },
  width:{
    type: String
  }
});
</script>

<style scoped>
.app-modal {
  position: fixed;
  transform: translate(-50%, -50%);
  left: 50%;
  max-height: 600px;
  top: 50%;
  background-color: white;
  z-index: -1;
  opacity: 0;
  overflow: auto;
  border-radius: 0.5rem;
}
.app-modal-show {
  /* width: 90%; */
  opacity: 1;
  z-index: 100;
}
::-webkit-scrollbar {
  display: none;
}
.app-modal__body {
  padding: 20px;
}

.app-modal-shadow {
  background-color: rgba(0, 0, 0, 0.5);
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}
</style>