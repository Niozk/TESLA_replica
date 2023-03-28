<template>
    <article>
        <NavBar />
        <!-- <TeslaButton text="hey" color="white" backgroundColor="#35383E"/>
        <TeslaButton text="Demo drive" color="#35383E" backgroundColor="#E7E7E6"/> -->
    </article>
</template>

<script setup>
    import NavBar from './NavBar.vue'
    // import TeslaButton from './TeslaButton.vue'
</script>

<style scoped>
    article {
        background: url(../assets/model-3.jfif); 
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        height: 100vh;
    }

    @media only screen 
	and (max-width: 600px) {
        article {
            background: url(../assets/model-3-mobile.jfif); 
            background-repeat: no-repeat;
            background-position: center;
            background-size: 110%;
        }
	}

    @media only screen 
	and (max-width: 375px) {
        article {
            background: url(../assets/model-3-mobile.jfif); 
            background-repeat: no-repeat;
            background-position: center;
            background-size: 385px;
        }
	}
</style>