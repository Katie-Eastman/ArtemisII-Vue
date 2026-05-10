<script setup>
    import Navbar from './components/Navbar.vue'
    import Main from './components/Main.vue'
    import Footer from './components/Footer.vue'
</script>

<template>

    <div class="app-wrapper">
        <Navbar />
        <Main class="app-main "/>
        <Footer />
    </div>

</template>

<style scoped>
    .app-wrapper {
        min-height: 100vh;
        display: flex;
        flex-direction: column;

        background-image: url("assets/space-bg.jpg");
        background-position: center;
        background-size: cover;
        background-repeat: no-repeat;
        background-attachment: fixed;
    }

    .app-main {
        flex: 1;
    }
</style>
