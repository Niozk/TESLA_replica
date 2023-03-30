<template>
    <div id="article-text" class="article-text">
        <h1> {{ currentItem  }}</h1>
        <p>Leasing starting at $349/mo</p>
    </div>
</template>

<script setup>
    import { ref, onMounted } from 'vue';

    const articleTextTitleItems = ['Model Y', 'Model S',  'Model X', 'Solar Panels', 'Solar Roof', 'Accessories'];
    const startingItem = 'Model 3';
    let currentItem = ref(startingItem);

    onMounted(() => {
        window.addEventListener('scroll', changeCurrentItem);
    });

    // function changeCurrentItem() {
    //     let scrollPosition = document.documentElement.scrollTop;
    //     currentItem.value = scrollPosition < 450 ? startingItem : itemBasedOnScrollPosition(scrollPosition);
    //     console.log(scrollPosition);
    // }

    // function itemBasedOnScrollPosition(scrollPosition) {
    //     const index = Math.floor((scrollPosition - 450) / 800) % articleTextTitleItems.length;
    //     const item = articleTextTitleItems[index];
    //     console.log(item);
    //     return item;
    // }

    function changeCurrentItem() {
        let scrollPosition = document.documentElement.scrollTop;
        let viewportHeight = window.innerHeight;
        let startingOffset = viewportHeight * 0.44;
        let itemOffset = viewportHeight;
        currentItem.value = scrollPosition < startingOffset ? startingItem : itemBasedOnScrollPosition(scrollPosition, startingOffset, itemOffset);
    }

    function itemBasedOnScrollPosition(scrollPosition, startingOffset, itemOffset) {
        const index = Math.floor((scrollPosition - startingOffset) / itemOffset) % articleTextTitleItems.length;
        const item = articleTextTitleItems[index];
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
		margin: 110px 36px 25px 36px;
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
        font-size: 20px;
    }

    @media only screen 
	and (max-width: 350px) {
        .article-text p {
            white-space: normal;
        }
	}
</style>