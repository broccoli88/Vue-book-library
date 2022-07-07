<template>
  <div class="home">
    <!-- HEADER -->

    <header class="top-panel flex">
      <span class="top-panel__brand">BOOKS</span>
      <div class="top-panel__search flex">
        <input type="text" />
        <SearchButton />
      </div>
    </header>

    <!-- ASIDE -->

    <aside class="aside-panel flex-column">
      <div class="search flex">
        <input type="text" />
        <SearchButton />
      </div>
    </aside>

    <!-- MAIN -->

    <!-- FOOTER -->
  </div>
</template>

<script setup>
import SearchButton from "../components/SearchButton.vue";
</script>
<style scoped>
.home {
  width: 100vw;
  min-height: 100vh;

  display: grid;
  grid-template-columns: minmax(20rem, 20vw) 1fr;
  grid-template-rows: auto 1fr auto;
  /* grid-template-areas:
  "header header"
  "aside main""
  "footer footer"; */
}

.top-panel {
  grid-column: 1 / 3;

  width: 100%;
  padding: 1rem 2rem;

  gap: 4rem;

  border-bottom: 2px solid var(--color-primary);
  box-shadow: var(--shadow);
}

.top-panel__brand {
  font-size: 2.5rem;
  font-weight: 800;
  color: var(--color-primary);
}

.top-panel__search {
  width: clamp(30rem, 35vw, 60rem);
}

input {
  width: 100%;

  font-size: 1.8rem;

  box-shadow: inset 0 0 2px grey;
  border: 0;
}
</style>
