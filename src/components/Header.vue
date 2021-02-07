<template>
  <div class="header">
    <router-link :to="'/'">
      <div class="brand">
        <div class="splash_header">
          <div>
            <img class="logo" :src="logo" />
          </div>
          <div class="splash_header_text">
            <h1 class="title">Reloaded</h1>
            <span>Version 1.0</span>
          </div>
        </div>
      </div>
    </router-link>
    <div class="header-right">
      <a class="link" href="https://pools.reloaded.exchange" target="_blank">
        Add Liquidity
      </a>
      <Account class="account" />
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

import logo from "@/assets/logo-mark-reloaded.svg";
import title from "@/assets/title.svg";

import Account from "@/components/Account.vue";

export default defineComponent({
  components: {
    Account,
  },
  setup() {
    return {
      logo,
      title,
    };
  },
});
</script>

<style scoped>
.header {
  margin: 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: var(--background-header);
}

.header-right {
  display: flex;
  align-items: center;
}

.link {
  margin-right: 8px;
}

a {
  text-decoration: none;
  color: var(--text-primary);
}

.splash_header {
  display: flex;
}

.splash_header_text {
  margin-left: 10px;
}

.brand {
  display: flex;
  align-items: center;
}

.logo {
  /* height: 40px;
    width: 40px; */
}

.title {
  margin-left: 16px;
  font-size: 20px;
  margin: 6px 0 0;
  font-size: 18px;
}

.account {
  margin-left: 8px;
}
</style>
