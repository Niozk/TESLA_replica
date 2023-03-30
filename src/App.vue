<template>
    <NavBar />
    <SideMenu />
    <ArticleText />
    <ArticleButtons />
    <div id="overlay"> <!-- in de overlay div kunnen alleen components en elements die geen fixed attribute hebben -->
        <ArticleCarousel />
    </div>
    <Footer />
</template>

<script setup>
    import NavBar from './components/NavBar.vue'
    import SideMenu from './components/SideMenu.vue'
    import ArticleCarousel from './components/ArticleCarousel.vue'
    import ArticleText from './components/ArticleText.vue'
    import ArticleButtons from './components/ArticleButtons.vue'
    import Footer from './components/Footer.vue'
</script>

<style scoped>
</style>