<template>
  <div id="app">
    <Header />
    <router-view class="view" />

    <ModalSettings :open="isSettingsModalOpen" />
    <ModalAccount :open="isAccountModalOpen" />
    <ModalConnectorSelector :open="isConnectorModalOpen" />
    <NotificationList :items="notifications" />
  </div>
</template>

<script lang="ts">
import { defineComponent, computed, onMounted } from "vue";
import { useStore } from "vuex";

import { RootState } from "@/store";

import Header from "@/components/Header.vue";
import ModalAccount from "@/components/ModalAccount.vue";
import ModalConnectorSelector from "@/components/ModalConnectorSelector.vue";
import ModalSettings from "@/components/ModalSettings.vue";
import NotificationList from "@/components/NotificationList.vue";

export default defineComponent({
  components: {
    Header,
    ModalAccount,
    ModalConnectorSelector,
    ModalSettings,
    NotificationList,
  },
  setup() {
    const store = useStore<RootState>();

    const isSettingsModalOpen = computed(
      () => store.state.ui.modal.settings.isOpen
    );
    const isAccountModalOpen = computed(
      () => store.state.ui.modal.account.isOpen
    );
    const isConnectorModalOpen = computed(
      () => store.state.ui.modal.connector.isOpen
    );

    const notifications = computed(() => store.state.ui.notifications);

    onMounted(() => {
      store.dispatch("assets/init");
      store.dispatch("account/init");
    });

    return {
      isSettingsModalOpen,
      isAccountModalOpen,
      isConnectorModalOpen,
      notifications,
    };
  },
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");

@font-face {
  font-family: "IBM VGA 8x14";
  font-style: normal;
  font-weight: 400;
  src: local(""), url("/src/assets/fonts/web-ibm-vga-8x14.woff") format("woff");
}

:root {
  --color-aquamarine: #76ffff;
  --color-bondi-blue: #06a9ad;
  --color-broom: #feff26;
  --color-dark-blue: #1100ad;
  --color-persimmon: #ff5655;
  --color-neutral-black: #000000;
  --color-neutral-dark-grey: #222222;
  --color-neutral-grey: #aaaaaa;
  --color-neutral-white: #ffffff;

  --color-brand-primary: var(--color-dark-blue);
  --color-brand-primary--light: var(--color-aquamarine);
  --color-brand-primary--mid: var(--color-bondi-blue);

  --background-primary: var(--color-neutral-black);
  --background-secondary: var(--color-bondi-blue);
  --background-header: var(--color-neutral-black);
  --background-form: #1f1f1f;
  --background-control: var(--color-neutral-dark-grey);
  --background-hover: var(--color-aquamarine);
  --border-form: var(--color-brand-primary--light);
  --border-input: var(--color-brand-primary--light);
  --accent: #4965ff;
  --accent-dark: #3c56e3;
  --text-primary: #fff;
  --text-secondary: #acbbc3;
  --text-control: #1100ad;
  --text-inverted: #000;
  --success: #21b66f;
  --info: #7685d5;
  --warning: var(--color-broom);
  --error: var(--color-persimmon);
  --font-size-tiny: 11px;
  --font-size-small: 14px;
  --font-size-medium: 16px;
  --font-size-large: 18px;
  --font-size-header: 24px;
  --border-radius-large: 0;
  --border-radius-medium: 0;
  --border-radius-small: 0;
  --block-height: 50px;
}

body {
  font-family: "IBM VGA 8x14", "Helvetica Neue", Helvetica, "Segoe UI", Arial,
    sans-serif;
  font-size: var(--font-size-medium);
  margin: 0;
  background: var(--background-primary);
  color: var(--text-primary);
}

input {
  appearance: textfield;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input:invalid {
  box-shadow: none;
}

.view {
  min-height: calc(100vh - 96px);
  display: flex;
  align-items: center;
  justify-content: center;
}

@media only screen and (max-width: 768px) {
  .view {
    min-height: initial;
  }
}
</style>
