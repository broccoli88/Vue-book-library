<template>
    <div class="main-tab">
        <p class="title">Ja, Inkwizytor</p>
        <p class="author">Author: Jacek Piekara</p>
        <p class="release">Release: 1988</p>

        <p class="description">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempora in
            perferendis eius voluptatem consequuntur itaque assumenda quidem
            libero dolor commodi corrupti nemo, debitis veritatis voluptas!
            Doloribus illo assumenda sequi quisquam.
        </p>

        <p class="price">15$</p>
    </div>
</template>
<script setup></script>
<style scoped>
.main-tab {
    width: 100%;

    padding: var(--padding-panel);

    display: grid;
    grid-template-columns: repeat(2, auto);
    grid-template-rows: auto;
    grid-template-areas:
        "title title "
        "author release"
        "description description"
        ". price";

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

.title {
    grid-area: title;

    font-size: 2.5rem;
    font-weight: 800;
}

.author,
.release {
    font-size: 1.8rem;
    font-weight: 600;
}

.author {
    grid-area: author;
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
