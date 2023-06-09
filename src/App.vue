<script setup>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';
</script>

<template>
    <Navbar />
    <RouterView />
    <Footer/>

</template>

<style>
body{
    @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');
    margin: 0;
    font-family: 'Roboto', sans-serif;
    background-color: #2d2d2d !important;
}
</style>
