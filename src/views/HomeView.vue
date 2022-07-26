<template>
    <div class="home">
        <!-- HEADER -->

        <header class="header-panel flex">
            <span class="header-panel__brand">BOOKS</span>
            <div class="header-panel__search flex">
                <input v-model="bookSearch" type="text" placeholder="title" />
                <!-- <SearchButton @search="searchBook" /> -->
            </div>
            <div class="header-panel__search flex">
                <input
                    v-model="authorSearch"
                    type="text"
                    placeholder="author"
                />
            </div>
            <SearchButton @search="searchBook" />
        </header>

        <!-- ASIDE -->

        <aside class="aside-panel flex-column">
            <div class="aside-panel__navigation flex-column">
                <NavigationButton>
                    <template v-slot="favorites"> favorites </template>
                </NavigationButton>
                <NavigationButton>
                    <template v-slot="myBooks"> my books </template>
                </NavigationButton>
                <NavigationButton>
                    <template v-slot="doneReading"> done reading </template>
                </NavigationButton>
                <NavigationButton>
                    <template v-slot="toRead"> to read </template>
                </NavigationButton>
            </div>
        </aside>

        <!-- MAIN -->

        <main class="main-panel">
            <MainTab
                @show-details="showDetails"
                :book="book"
                v-for="book in bookSearchList"
                :key="book.id"
            ></MainTab>
            <BookDetails v-if="isDetails" @close-details="hideDetails" />
        </main>

        <!-- FOOTER -->
        <footer class="footer-panel">
            <a href="https://developers.google.com/books"
                >Google Book Store API</a
            >
        </footer>
    </div>
</template>

<script setup>
import SearchButton from "../components/SearchButton.vue";
import NavigationButton from "../components/NavigationButton.vue";
import MainTab from "../components/MainTab.vue";
import BookDetails from "../components/BookDetails.vue";
import { reactive, ref } from "vue";

// API
const bookSearchList = reactive([]);
const bookSearch = ref("");
const authorSearch = ref("");

const getData = async () => {
    if (bookSearchList.length > 0) {
        bookSearchList.splice(0, bookSearchList.length);
    }

    let response;

    if (bookSearch.value !== "" && authorSearch.value !== "") {
        response = await fetch(
            `https://www.googleapis.com/books/v1/volumes?q=${bookSearch.value}+inauthor:${authorSearch.value}`
        );
    } else if (bookSearch.value !== "" && authorSearch.value === "") {
        response = await fetch(
            `https://www.googleapis.com/books/v1/volumes?q=${bookSearch.value}`
        );
    } else if (bookSearch.value === "" && authorSearch.value !== "") {
        response = await fetch(
            `https://www.googleapis.com/books/v1/volumes?q=inauthor:${authorSearch.value}`
        );
    }

    const data = await response.json();
    data.items.forEach((item) => {
        bookSearchList.push(item);
    });
};

const searchBook = () => {
    getData();
};

// Book Details

const props = defineProps(["book"]);
const bookInfo = props.book;

const isDetails = ref(true);
const showDetails = (book) => {
    isDetails.value = true;
};

const hideDetails = () => {
    isDetails.value = false;
};
</script>

<style scoped>
.home {
    width: 100vw;
    min-height: 100vh;

    display: grid;
    grid-template-columns: minmax(20rem, 22vw) 1fr;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "header header"
        "aside main"
        "footer footer";
}

.header-panel {
    grid-area: header;

    width: 100%;
    padding: var(--padding-panel);

    gap: 2rem;

    border-bottom: 2px solid var(--color-primary);
    box-shadow: var(--shadow);
}

.header-panel__brand {
    font-size: 2.5rem;
    font-weight: 800;
    color: var(--color-primary);
}

.header-panel__search {
    width: clamp(30rem, 35vw, 60rem);
}

input {
    width: 100%;
    padding: 0 1rem;
    font-size: 1.8rem;

    box-shadow: inset 0 0 2px grey;
    border: 0;
}

.aside-panel {
    grid: aside;
    margin: 1.5rem 0;

    border-right: 1px solid var(--color-primary);
    box-shadow: 7px 0 5px -5px hsla(0, 0%, 0%, 0.2);

    gap: 2rem;
}

.aside-panel__search {
    padding: var(--padding-panel);
}

.main-panel {
    grid-area: main;
    position: relative;
}

.footer-panel {
    grid-area: footer;

    padding: 1rem 0;
    background-color: var(--color-primary);

    text-align: center;
}

.footer-panel > a {
    color: white;
}
</style>
