<template>
    <div class="search-button">
        <button @click="searchTerm">
            <Icon
                icon="entypo:magnifying-glass"
                color="var(--color-bg)"
                width="24"
                height="24"
                :inline="true"
            />
        </button>
    </div>
</template>
<script setup>
import { Icon } from "@iconify/vue";
import { defineEmits } from "vue";

const emits = defineEmits(["search"]);

const searchTerm = () => {
    emits("search");
};
</script>
<style scoped>
.search-button button {
    height: 100%;
    padding: 0 1rem;

    background-color: var(--color-primary);
    border: 0;
}

.search-button button:active {
    filter: brightness(115%);
}
</style>
