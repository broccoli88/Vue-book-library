<template>
    <div class="home">
        <!-- HEADER -->

        <header class="header-panel flex">
            <span class="header-panel__brand">BOOKS</span>
            <div class="header-panel__search flex">
                <input type="text" />
                <SearchButton />
            </div>
        </header>

        <!-- ASIDE -->

        <aside class="aside-panel flex-column">
            <div class="aside-panel__search flex">
                <input type="text" />
                <SearchButton />
            </div>
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
            <MainTab></MainTab>
        </main>

        <!-- FOOTER -->
        <footer class="footer-panel">
            <h2>Footer</h2>
        </footer>
    </div>
</template>

<script setup>
import SearchButton from "../components/SearchButton.vue";
import NavigationButton from "../components/NavigationButton.vue";
import MainTab from "../components/MainTab.vue";
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

    gap: 4rem;

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
}

.footer-panel {
    grid-area: footer;
}
</style>
