<template>
    <div class="main-tab">
        <figure class="cover">
            <img :src="bookInfo.imageLinks.smallThumbnail" alt="" />
        </figure>
        <p class="title">{{ bookInfo.title }}</p>
        <p class="author">{{ bookInfo.authors[0] }}</p>
        <p class="publisher">{{ bookInfo.publisher }}</p>
        <p class="release">Released: {{ bookInfo.publishedDate }}</p>

        <p class="description">
            {{ bookInfo.description }}
        </p>

        <p class="price">
            {{ bookPriceInfo.retailPrice.amount }}
            {{ bookPriceInfo.retailPrice.currencyCode }}
        </p>
    </div>
</template>
<script setup>
import { reactive } from "vue";

const props = defineProps(["book"]);
const bookInfo = reactive(props.book.volumeInfo);
const bookPriceInfo = reactive(props.book.saleInfo);

console.log(bookInfo);
</script>
<style scoped>
.main-tab {
    width: 100%;

    padding: var(--padding-panel);

    display: grid;
    grid-template-columns: repeat(3, auto);
    grid-template-rows: auto;
    grid-template-areas:
        "cover title title "
        "author publisher release"
        "description description description"
        ". . price";

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

.price {
    grid-area: price;

    font-size: 3rem;
    font-weight: 600;

    justify-self: end;
}
</style>
