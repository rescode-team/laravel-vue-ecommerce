<template>
    <div class="relative">
        <div
            v-if="!state.firstRender"
            class="fixed top-0 left-0 z-50 w-screen mt-36 bg-white h-screen animate__animated"
            :class="{
                animate__fadeInLeft: state.expandedMenu,
                animate__fadeOutRight:
                    !state.expandedMenu && !state.firstRender,
            }"
        >
            <ul class="z-50">
                <li
                    class="z-50 text-xl w-auto p-4 m-4 font-bold text-center border border-gray-300 border-opacity-50 shadow-md rounded"
                >
                    <router-link to="/" @click="displayMobileMenu">
                        Home
                    </router-link>
                </li>
                <li
                    class="z-50 text-xl w-auto p-4 m-4 font-bold text-center border border-gray-300 border-opacity-50 shadow-md rounded"
                >
                    <router-link to="/products" @click="displayMobileMenu">
                        Products
                    </router-link>
                </li>
            </ul>
        </div>
        <div class="w-5/12 lg:hidden" />
        <div class="flex flex-row w-2/12 px-2 py-2 ml-8 lg:hidden">
            <div class="self-center block w-full mr-4">
                <button
                    id="nav-toggle"
                    class="mt-2 burger burger-squeeze"
                    aria-haspopup="true"
                    :aria-expanded="state.expandedMenu"
                    aria-controls="menu"
                    aria-label="Navigation"
                    :class="{ open: state.expandedMenu }"
                    @click="displayMobileMenu"
                >
                    <div class="burger-lines" />
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { reactive } from "vue";

const state = reactive({ expandedMenu: false, firstRender: true });

const displayMobileMenu = () => {
    state.expandedMenu = !state.expandedMenu;
    state.firstRender = false;
};
</script>

<style scoped>
/* Main hamburger styling */
.burger {
    height: 3em;
    width: 3em;
    position: relative;
    font-size: 14px;
    cursor: pointer;
    transition: 0.5s all;
    -webkit-tap-highlight-color: transparent;
}

.burger .burger-lines::after {
    left: 0;
    top: -1em;
}

.burger .burger-lines::before {
    left: 1em;
    top: 1em;
}

.burger::after {
    content: "";
    display: block;
    position: absolute;
    height: 150%;
    width: 150%;
    top: -25%;
    left: -25%;
}

.burger .burger-lines {
    top: 50%;
    margin-top: -0.125em;
}

.burger .burger-lines,
.burger .burger-lines::after,
.burger .burger-lines::before {
    pointer-events: none;
    display: block;
    content: "";
    width: 100%;
    border-radius: 0.25em;
    background-color: #000;
    height: 0.25em;
    position: absolute;
    transform: rotate(0);
}

/* Burger animations classes */
.burger.burger-squeeze .burger-lines,
.burger.burger-squeeze .burger-lines::after,
.burger.burger-squeeze .burger-lines::before {
    transition: 0.2s top 0.2s, 0.1s left, 0.2s transform,
        0.4s background-color 0.2s;
}

.burger.burger-squeeze .burger-lines::after,
.burger.burger-squeeze .burger-lines::before {
    width: 2em;
}

.burger.burger-squeeze.open .burger-lines,
.burger.burger-squeeze.open .burger-lines::after,
.burger.burger-squeeze.open .burger-lines::before {
    transition: 0.2s background-color, 0.2s top, 0.2s left, 0.2s transform 0.15s;
}

.burger.burger-squeeze.open .burger-lines {
    background-color: transparent;
}

.burger.burger-squeeze.open .burger-lines::before,
.burger.burger-squeeze.open .burger-lines::after {
    left: 0.5em;
    top: 0;
}

.burger.burger-squeeze.open .burger-lines::before {
    transform: rotate(-45deg);
}

.burger.burger-squeeze.open .burger-lines::after {
    transform: rotate(45deg);
}
</style>
