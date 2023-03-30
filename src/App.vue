<template>
    <NavBar />
    <SideMenu />
    <ArticleText />
    <div id="overlay"> <!-- in de overlay div kunnen alleen components en elements die geen fixed attribute hebben -->
        <ArticleCarousel />
        <p>TESTESTEST</p>
    </div>
</template>

<script setup>
    import NavBar from './components/NavBar.vue'
    import SideMenu from './components/SideMenu.vue'
    import ArticleCarousel from './components/ArticleCarousel.vue'
    import ArticleText from './components/ArticleText.vue'
</script>

<style scoped>
</style>