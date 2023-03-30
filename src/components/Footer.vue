<template>
    <footer id="footer" class="footer">
        <ul>
            <div class="footerItems" v-if="!mobileView">
                <li v-for="item in footerItems" :key="item"><a href="#">{{ item }}</a></li>
            </div>
            <div class="footerItemsMobile" v-if="mobileView">
                <li v-for="item in footerItemsMobile" :key="item"><a href="#">{{ item }}</a></li>
            </div>
        </ul>
    </footer>
</template>

<script setup>
    import { ref, onMounted } from 'vue';
    const footerItems = ['Tesla © 2023', 'Privacy & Legal', 'Vehicle Recalls', 'News', 'Careers', 'Contact', 'Engage', 'Locations'];
    const footerItemsMobile = ['Tesla © 2023', 'Privacy & Legal', 'Vehicle Recalls', 'News', 'Careers']
    const mobileView = ref(window.innerWidth <= 600);

    onMounted(() => {
		window.addEventListener('resize', () => {
			mobileView.value = window.innerWidth <= 600;
		});
        window.addEventListener('scroll', handleScroll);
	});

    function handleScroll() {
		const footer = document.getElementById("footer");
        const scrollPosition = window.innerHeight + window.pageYOffset;
        const documentHeight = document.documentElement.offsetHeight;
        const footerPosition = documentHeight - footer.offsetHeight - 200;
        
        if (scrollPosition >= footerPosition) {
            footer.style.display = 'flex';
        } else {
            footer.style.display = 'none';
        }
    }
</script>

<style scoped>
    footer {
        display: flex;
		justify-content: center;
		position: fixed;
		z-index: 1;
		left: 0;
		right: 0;
        bottom: 10px;
		/* margin: 92vh 0 0 0; */
		padding: 0;
        text-align: center;
    }

    ul {
        padding: 0;
    }

    .footerItems {
        display: flex;
        gap: 14px;
    }

    .footerItemsMobile {
        display: flex;
        gap: 8px;
    }

	a {
		white-space: nowrap;
		text-decoration: none;
        font-size: 12px;
        font-weight: bold;
		color: #707172;
	}

    li {
		list-style-type: none;
		border-radius: 5px;
    }

    @media only screen 
	and (max-width: 700px) {
        footer {
            position: initial;
        }
    }

    @media only screen 
	and (max-width: 400px) {
        .footerItemsMobile {
            display: flex;
            flex-direction: column;
        }
    }
</style>