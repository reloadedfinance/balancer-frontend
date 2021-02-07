<template>
  <transition name="appear">
    <div v-if="open" class="modal-wrapper">
      <div class="backdrop" @click="$emit('close')" />
      <div class="modal">
        <div class="header">
          <div>
            {{ title }}
          </div>
          <Button :text="'close'" :primary="false" @click="$emit('close')" />
          <!-- <Icon class="close-icon" :title="'close'" @click="$emit('close')" /> -->
        </div>
        <div class="body">
          <slot />
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import { defineComponent } from "vue";

import Icon from "@/components/Icon.vue";
import Button from "@/components/Button.vue";

export default defineComponent({
  components: {
    Icon,
    Button,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    open: {
      type: Boolean,
      required: true,
    },
  },
  emits: ["close"],
});
</script>

<style scoped>
.modal-wrapper {
  position: fixed;
  display: flex;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  align-items: center;
  justify-content: center;
  z-index: 1;
}

.backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 2;
  background: rgba(0, 0, 0, 0.8);
}

.modal {
  color: var(--color-neutral-black);
  width: 440px;
  max-height: 90%;
  z-index: 3;
  padding: 20px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  position: relative;
  background: var(--color-brand-primary--light);
}

.modal::before {
  border: 2px solid var(--color-neutral-dark-grey);
  bottom: 0;
  box-sizing: border-box;
  content: "";
  left: 0;
  margin: auto;
  position: absolute;
  right: 0;
  top: 0;
  height: calc(100% - 10px);
  width: calc(100% - 10px);
  z-index: -1;
}
.modal::after {
  border: 2px solid var(--color-neutral-dark-grey);
  bottom: 0;
  box-sizing: border-box;
  content: "";
  left: 0;
  margin: auto;
  position: absolute;
  right: 0;
  top: 0;
  height: calc(100% - 20px);
  width: calc(100% - 20px);
  z-index: -1;
}

.header {
  min-height: 40px;
  box-sizing: border-box;
  padding: 0 16px;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  font-size: 22px;
  font-weight: bold;
}

.close-icon {
  width: 16px;
  cursor: pointer;
}

.body {
  overflow-y: auto;
}

@media only screen and (max-width: 768px) {
  .modal-wrapper {
    align-items: flex-start;
  }

  .modal {
    border-radius: 0;
    max-height: 100%;
  }
}
</style>
