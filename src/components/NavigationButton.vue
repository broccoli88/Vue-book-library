<template>
    <div class="navigation-button">
        <button class="flex">
            <a class="link" href="#">
                <slot></slot>
            </a>
        </button>
    </div>
</template>
<script setup></script>

<style scoped>
button {
    width: 100%;
    background-color: transparent;
    background-position: 0%;

    border: 0;

    padding: 1em 2rem;

    cursor: pointer;

    position: relative;
    z-index: 1;
}

button::before {
    content: "";
    display: inline-block;

    background-color: var(--color-primary);

    position: absolute;
    width: 0;
    height: 100%;
    top: 0;
    left: 0;
    z-index: 0;

    transition: all 0.3s ease-in;
}

button:hover::before {
    width: 100%;
}

.link {
    font-size: 1.8rem;
    font-weight: 600;
    color: var(--color-font);
    text-transform: capitalize;

    z-index: 1;
    transition: all 0.3s ease-in;
}

button:hover > .link {
    color: white;
}
</style>
