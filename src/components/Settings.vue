<template>
    <Button
        :text="'Settings'"
        :primary="false"
        @click="openSettingsModal"
    />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { useStore } from 'vuex';

import { RootState } from '@/store';

import Button from '@/components/Button.vue';

export default defineComponent({
    components: {
        Button,
    },
    setup() {
        const store = useStore<RootState>();

        function openSettingsModal(): void {
            store.dispatch('ui/openSettingsModal');
        }

        return {
            openSettingsModal,
        };
    },
});
</script>

