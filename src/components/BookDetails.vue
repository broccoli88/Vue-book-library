<template>
    <!-- <Teleport to=".main-panel"> -->
    <div class="book-details">
        <h1>Title</h1>
        <div class="basic-informations">
            <span class="author">Author</span>
            <span class="publisher">Publisher</span>
            <span class="release-date">Release date</span>
        </div>
        <button @click="close">Close</button>
    </div>
    <!-- </Teleport> -->
</template>
<script setup>
import { reactive } from "vue";

const emits = defineEmits(["close-details"]);

const close = () => {
    emits("close-details");
};
</script>
<style scoped>
.book-details {
    background-color: var(--color-bg);

    width: 100%;
    height: 100%;

    position: absolute;
    top: 0;
    left: 0;
    z-index: 9;
}
</style>
