<template>
    <div id="article-text" class="article-text">
        <h1>{{ currentTitle }}</h1>
        <p>{{ currentDesc }}</p>
    </div>
</template>

<script setup>
    import { ref, onMounted } from 'vue';

    const articleTextTitleItems = ['Model Y', 'Model S',  'Model X', 'Solar Panels', 'Solar Roof', 'Accessories'];
    const articleTextDescItems = ['Schedule a Demo Drive', 'Schedule a Demo Drive',  'Schedule a Demo Drive',
     'Lowest Cost Solar Panels in America', 'Produce Clean Energy From Your Roof', ''];
    const startingTitle = 'Model 3';
    const startingDesc = 'Leasing starting at $349/mo';
    let currentTitle = ref(startingTitle);
    let currentDesc = ref(startingDesc);

    onMounted(() => {
        window.addEventListener('scroll', changeCurrentItem);
    });

    function changeCurrentItem() {
        let scrollPosition = document.documentElement.scrollTop;
        let viewportHeight = window.innerHeight;
        let startingOffset = viewportHeight * 0.44;
        let itemOffset = viewportHeight;
        currentTitle.value = scrollPosition < startingOffset ? startingTitle :
         itemBasedOnScrollPosition(scrollPosition, startingOffset, itemOffset, articleTextTitleItems);
        currentDesc.value = scrollPosition < startingOffset ? startingDesc :
         itemBasedOnScrollPosition(scrollPosition, startingOffset, itemOffset, articleTextDescItems);
    }

    function itemBasedOnScrollPosition(scrollPosition, startingOffset, itemOffset, itemList) {
        const index = Math.floor((scrollPosition - startingOffset) / itemOffset) % itemList.length;
        const item = itemList[index];
        return item;
    }
</script>

<style scoped>
    .article-text {
        display: flex;
		justify-content: center;
        flex-direction: column;
		position: fixed;
		z-index: 1;
		top: 0;
		left: 0;
		right: 0;
		margin: 110px 36px 0 36px;
		padding: 0;
        color: red;
        text-align: center;
    }

    .article-text h1 {
        margin: 0;
        white-space: nowrap;
        font-size: 44px;
    }

    .article-text p {
        margin: 10px 0;
        white-space: nowrap;
        font-size: 18px;
    }

    @media only screen 
	and (max-width: 600px) {
        .article-text h1 {
            font-size: 36px;
        }
    }

    @media only screen 
	and (max-width: 350px) {
        .article-text p {
            white-space: normal;
        }
	}
</style>