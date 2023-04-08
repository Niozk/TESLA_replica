<template>
    <article class="model-3 background-model"></article>
    <article class="model-y background-model"></article>
    <article class="model-s background-model"></article>
    <article class="model-x background-model"></article>
    <article class="solar-panels background-model"></article>
    <article class="solar-roof background-model"></article>
    <article class="accessories background-model"></article>
</template>

<script setup>
    import { onMounted } from 'vue';

    onMounted(() => {
        const backgroundModels = document.querySelectorAll('.background-model');
        const scrollDistance = 350;
        let isAutoScrolling = false;
        let scrollTimeout = null;

        window.addEventListener('scroll', () => {
            if (isAutoScrolling) return;

            clearTimeout(scrollTimeout);
            scrollTimeout = setTimeout(() => {
                for (let i = 0; i < backgroundModels.length; i++) {
                    const backgroundModel = backgroundModels[i];
                    const distanceFromTop = backgroundModel.offsetTop - window.scrollY;
                    const distanceFromBottom = distanceFromTop + backgroundModel.offsetHeight - window.innerHeight;

                    if (distanceFromTop <= scrollDistance && distanceFromBottom >= -75) {
                        isAutoScrolling = true;
                        const elementPosition = backgroundModel.getBoundingClientRect().top + window.pageYOffset;
                        window.scrollTo({ top: elementPosition, behavior: 'smooth' });

                        setTimeout(() => {
                            isAutoScrolling = false;
                        }, 1000);
                    }
                }
            }, 500);
        });
    });
</script>

<style scoped>
    body .background-model {
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        height: 100vh;
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

    .solar-panels {
        background: url(../assets/solar-panels.jfif); 
    }

    .solar-roof {
        background: url(../assets/solar-roof.jpg); 
    }

    .accessories {
        background: url(../assets/accessories.jpg); 
    }

    @media only screen 
	and (max-width: 600px) {
        body .background-model {
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

        .solar-panels {
            background: url(../assets/solar-panels-mobile.jpg); 
        }

        .solar-roof {
            background: url(../assets/solar-roof-mobile.jpg); 
        }

        .accessories {
            background: url(../assets/accessories-mobile.jpg); 
        }
	}

    @media only screen 
	and (max-width: 375px) {
        body .background-model {
            background-repeat: no-repeat;
            background-position: center;
            background-size: 385px;
        }
	}
</style>