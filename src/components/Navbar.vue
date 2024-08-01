<script setup>
import logo from "@/assets/img/olympic-logo.svg";
</script>

<template>
    <nav class="font-sans flex flex-col text-center content-center sm:flex-row sm:text-left sm:justify-between py-2 px-6 bg-white shadow sm:items-baseline w-full">

        <div class="mb-2 sm:mb-0 flex flex-row">
            <div class="h-10 w-10 self-center mr-2">
                <img class="h-10 w-10 self-center" v-bind:src="logo" />
            </div>
            <div>
                <a href="/home" class="text-2xl no-underline text-grey-darkest hover:text-blue-dark font-sans font-bold">Jeux Olympique 2024</a><br>
                <span class="text-xs text-grey-dark">
                    Toutes les informations sur Paris 2024</span>
            </div>
        </div>

        <div class="sm:mb-0 self-center">
                <RouterLink to="/">Home</RouterLink> |
                <RouterLink to="/about">About</RouterLink>
        </div>
    </nav>
</template>

<style scoped>

</style>
