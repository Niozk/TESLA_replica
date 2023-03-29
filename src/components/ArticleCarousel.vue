<template>
    <div class="article-text">
        <h1>{{ currentItem }}</h1>
        <p>Leasing starting at $349/mo</p>
        <!-- <button @click="manier">hey</button> -->
    </div>
    <article class="model-3 car-model">
        <NavBar />
        <!-- <TeslaButton text="hey" color="white" backgroundColor="#35383E"/>
        <TeslaButton text="Demo drive" color="#35383E" backgroundColor="#E7E7E6"/> -->
    </article>
    <article class="model-y car-model"></article>
    <article class="model-s car-model"></article>
    <article class="model-x car-model"></article>
</template>

<script setup>
    import { ref, onMounted } from 'vue';
    import NavBar from './NavBar.vue'
    // import TeslaButton from './TeslaButton.vue'

	const articleTextTitleItems = ['Model Y', 'Model S',  'Model X', 'Solar Panels', 'Solar Roof', 'Accessories'];
    const startingItem = 'Model 3';
    let currentItem = ref(startingItem);

    onMounted(() => {
        window.addEventListener('scroll', changeCurrentItem);
    });

    function changeCurrentItem() {
        let scrollPosition = document.documentElement.scrollTop;
        currentItem.value = scrollPosition < 450 ? startingItem : itemBasedOnScrollPosition(scrollPosition);
        console.log(scrollPosition);
    }

    function itemBasedOnScrollPosition(scrollPosition) {
        const index = Math.floor((scrollPosition - 450) / 800) % articleTextTitleItems.length;
        const item = articleTextTitleItems[index];
        console.log(item);
        return item;
    }
</script>

<style scoped>
    body .car-model {
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        height: 100vh;
    }

    .article-text {
        position: fixed;
        top: 110px;
        left: 50%;
        transform: translate(-50%, 0);
        text-align: center;
        color: red;
    }

    .article-text h1 {
        margin: 0;
        white-space: nowrap;
        font-size: 44px;
    }

    .article-text p {
        margin: 10px 0;
        font-size: 20px;
    }

    .model-3 {
        background: url(../assets/model-3.jfif); 
    }

    .model-y {
        background: url(../assets/model-y.jpg); 
    }

    .model-s {
        background: url(../assets/model-s.jfif); 
    }

    .model-x {
        background: url(../assets/model-x.jfif); 
    }

    @media only screen 
	and (max-width: 600px) {
        body .car-model {
            background-repeat: no-repeat;
            background-position: center;
            background-size: 110%;
        }

        .article-text p {
            white-space: nowrap;
        }

        .model-3 {
            background: url(../assets/model-3-mobile.jfif); 
        }

        .model-y {
            background: url(../assets/model-y-mobile.jfif); 
        }

        .model-s {
            background: url(../assets/model-s-mobile.jfif); 
        }

        .model-x {
            background: url(../assets/model-x-mobile.jfif); 
        }
	}

    @media only screen 
	and (max-width: 375px) {
        body .car-model {
            background-repeat: no-repeat;
            background-position: center;
            background-size: 385px;
        }
	}

    @media only screen 
	and (max-width: 325px) {
        .article-text p {
            white-space: normal;
        }
	}
</style>