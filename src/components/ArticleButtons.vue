<template>
    <div id="article-buttons" class="article-buttons">
        <TeslaButton :text="currentButtonBlack" color="white" backgroundColor="#35383E"/>
        <TeslaButton :text="currentButtonWhite" color="#35383E" backgroundColor="#E7E7E6" v-if="accessoriesView"/>
    </div>
</template>

<script setup>
    import { ref, onMounted } from 'vue';
    import TeslaButton from './TeslaButton.vue';

    const articleButtonBlackItem = ['View Inventory', 'View Inventory', 'View Inventory', 'Order Now', 'Order Now', 'Shop Now'];
    const articleButtonWhiteItem = ['Custom Order', 'Custom Order', 'Custom Order', 'Learn More', 'Learn More', ''];
    const startingButtonBlack = 'View Inventory';
    const startingButtonWhite = 'Custom Order';
    let currentButtonBlack = ref(startingButtonBlack);
    let currentButtonWhite = ref(startingButtonWhite);
    const accessoriesView = ref(true);
    const accessoriesMobileWidth = ref();

    onMounted(() => {
        window.addEventListener('resize', () => {
			accessoriesMobileWidth.value = window.innerWidth <= 400;
		});
        window.addEventListener('scroll', changeCurrentItem);
        window.addEventListener('scroll', handleScroll);
	});

    function handleScroll() {
		const footer = document.getElementById("footer");
        const articleButtons = document.getElementById("article-buttons");
        const scrollPosition = window.innerHeight + window.pageYOffset;
        const documentHeight = document.documentElement.offsetHeight;
        const footerPosition = documentHeight - footer.offsetHeight - 400;
        
        if (scrollPosition >= footerPosition) {
            accessoriesView.value = false;
            if (accessoriesMobileWidth.value) {
                articleButtons.style.margin = "500px 36px 0 36px";
            }
        } else {
            accessoriesView.value = true;
            articleButtons.style.margin = "600px 36px 0 36px";
        }
    }

    function changeCurrentItem() {
        let scrollPosition = document.documentElement.scrollTop;
        let viewportHeight = window.innerHeight;
        let startingOffset = viewportHeight * 0.44;
        let itemOffset = viewportHeight;
        currentButtonBlack.value = scrollPosition < startingOffset ? startingButtonBlack :
        itemBasedOnScrollPosition(scrollPosition, startingOffset, itemOffset, articleButtonBlackItem);
        currentButtonWhite.value = scrollPosition < startingOffset ? startingButtonWhite :
        itemBasedOnScrollPosition(scrollPosition, startingOffset, itemOffset, articleButtonWhiteItem);
    }

    function itemBasedOnScrollPosition(scrollPosition, startingOffset, itemOffset, itemList) {
        const index = Math.floor((scrollPosition - startingOffset) / itemOffset) % itemList.length;
        const item = itemList[index];
        return item;
    }
</script>

<style scoped>
    .article-buttons {
        display: flex;
        justify-content: center;
        position: fixed;
        z-index: 1;
        top: 0;
        left: 0;
        right: 0;
        margin: 600px 36px 0 36px;
        text-align: center;
    }

    @media only screen 
	and (max-width: 520px) {
        .article-buttons {
            justify-content: space-between;
            align-items: center;
            flex-direction: column;
            gap: 15px;
            margin: 565px 26px 0 26px;
        }
    }

    @media only screen 
    and (max-height: 720px) {
        .article-buttons {
            margin: 450px 26px 0 26px;
        }
    }

    @media only screen 
    and (max-height: 550px) {
        .article-buttons {
            margin: 350px 26px 0 26px;
        }
    }
</style>