<template>
    <div class="main-tab">
        <figure v-if="bookInfo.imageLinks" class="cover">
            <img :src="bookInfo.imageLinks.smallThumbnail" alt="" />
        </figure>
        <p class="title" v-if="bookInfo.title">{{ bookInfo.title }}</p>
        <p class="author" v-if="bookInfo.authors">
            {{ bookInfo.authors[0] }}
        </p>
        <p class="publisher" v-if="bookInfo.publisher">
            {{ bookInfo.publisher }}
        </p>
        <p class="release">Released: {{ bookInfo.publishedDate }}</p>

        <p class="description" v-if="bookInfo.description">
            {{ bookDescription }} ...
        </p>

        <button class="details">Details</button>
    </div>
</template>
<script setup>
import { computed } from "@vue/reactivity";
import { reactive } from "vue";

const props = defineProps(["book"]);
const bookInfo = reactive(props.book.volumeInfo);
const bookPriceInfo = reactive(props.book.saleInfo);

const bookDescription = computed(() => {
    if (!bookInfo.description) return;
    return bookInfo.description.substring(0, 455);
});
</script>
<style scoped>
.main-tab {
    width: 100%;

    padding: 3rem 2rem;

    display: grid;
    grid-template-columns: repeat(3, auto);
    grid-template-rows: auto;
    grid-template-areas:
        "cover title title "
        "author publisher release"
        "description description description"
        ". . details";

    position: relative;
}

.main-tab::after {
    content: "";
    display: inline-block;
    background-color: var(--color-primary);

    position: absolute;
    width: 80%;
    height: 1px;
    bottom: 0;
    left: 10%;
}

.main-tab > p {
    padding: 1rem 0;
}

.cover {
    grid-area: cover;
}

.title {
    grid-area: title;

    font-size: 2.5rem;
    font-weight: 800;
}

.author,
.release,
.publisher {
    font-size: 1.8rem;
    font-weight: 600;

    justify-self: start;
}

.author {
    grid-area: author;
}

.publisher {
    grid-area: publisher;
}

.release {
    grid-area: release;
}

.description {
    grid-area: description;
}

.details {
    grid-area: details;

    margin: 2rem 0;
    background-color: transparent;
    border: 0;

    font-size: 2rem;
    font-weight: 600;

    cursor: pointer;

    justify-self: end;
}
</style>
