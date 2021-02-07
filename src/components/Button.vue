<template>
  <button :class="{ primary }">
    <LoadingIndicator v-if="loading" />
    {{ text }}
  </button>
</template>

<script>
import { defineComponent } from "vue";

import LoadingIndicator from "@/components/LoadingIndicator.vue";

export default defineComponent({
  components: {
    LoadingIndicator,
  },
  props: {
    text: {
      type: String,
      required: true,
    },
    primary: {
      type: Boolean,
      default: false,
    },
    loading: {
      type: Boolean,
      default: false,
    },
  },
});
</script>

<style scoped>
button {
  cursor: pointer;
  display: block;
  width: auto;
  border: 0;
  padding: 0 2px;
  font-family: "IBM VGA 8x14", "Helvetica Neue", Helvetica, "Segoe UI", Arial,
    sans-serif;
  font-size: 18px;
  font-weight: normal;
  letter-spacing: 0.02em;
  line-height: 24px;

  background: var(--color-neutral-grey);
  color: var(--color-brand-primary);
}

button:hover,
button:active,
button:active:focus {
  background: var(--color-broom);
  color: var(--color-brand-primary);
}

button.primary {
  /* background: linear-gradient(185deg, var(--color-persimmon) -100%, var(--color-dark-blue) 100%) 40% / 200%; */
  /* transition: background 0.25s ease-in; */
}

button.primary:hover {
  /* background: linear-gradient(185deg, #f0f -100%, #00f 100%) 70% / 200%; */
}

button:disabled,
button:disabled:hover {
  background: var(--color-neutral-grey);
  cursor: not-allowed;
  opacity: 0.5;
}
</style>
