<template>
    	<aside id="sidemenu">
        <button class="close-btn" @click="closeSidemenu()">&times;</button>
		<ul>
			<div v-if="!isNavVisible">
				<li v-for="item in navList2Items" :key="item"><a href="#">{{ item }}</a></li>
			</div>
			<li v-for="item in asideItems" :key="item"><a href="#">{{ item }}</a></li>
			<div v-if="!isNavVisible">
				<li v-for="item in navList3Items" :key="item"><a href="#">{{ item }}</a></li>
			</div>
			<li><a href="#" class="language"><img class="language-img" src="../assets/world_icon.png" alt="World Icon">
				<p class="language-country">United States</p><p class="language-spoken">English</p></a></li>
		</ul>
    </aside>
</template>

<script setup>
    import { ref, onMounted } from 'vue';
    const asideItems = ref(['Existing Inventory', 'Used Inventory', 'Trade-In', 'Demo Drive', 'Insurance', 'Commercial Energy',
		'Utilities', 'Charging', 'Find Us', 'Support', 'Investor Relations']);
    const navList2Items = ref(['Model S', 'Model 3', 'Model X', 'Model Y', 'Solar Roof', 'Solar Panels', 'Powerwall']);
	const navList3Items = ref(['Shop', 'Account']);
    const isNavVisible = ref(window.innerWidth >= 1200);

    onMounted(() => {
		window.addEventListener('resize', () => {
			isNavVisible.value = window.innerWidth >= 1200;
		});
	});

	function closeSidemenu() {
		const sidemenu = document.getElementById("sidemenu");
		const nav = document.getElementById("nav");
		const overlay = document.getElementById("overlay");
		const articleText = document.getElementById("article-text");
		const footer = document.getElementById("footer");
		const articleButtons = document.getElementById("article-buttons");

		sidemenu.style.width = "0";
		sidemenu.style.opacity = "0";

		overlay.style.filter = "blur(0px)";
		nav.style.filter = "blur(0px)";
		articleText.style.filter = "blur(0px)";
		footer.style.filter = "blur(0px)";
		articleButtons.style.filter = "blur(0px)";

		setTimeout(() => {
			sidemenu.style.boxShadow = "0";
			document.body.style.overflow = "auto";
			document.body.style.marginRight = "0";

			nav.style.right = '';
			articleText.style.right = '';
			footer.style.right = '';
			articleButtons.style.right = '';
			sidemenu.classList.remove("show");
		}, 500);
	}
</script>

<style scoped>
    aside {
		display: flex;
		flex-direction: column; 
		position: fixed;
		z-index: 2;
		top: 0;
		right: 0;
		width: 0;
		height: 100%;
		overflow-x: hidden;
		background-color: white;
		transition: 1s;
		opacity: 0;
		font-size: 16px;
		font-weight: bold;
	}

	a {
		white-space: nowrap;
		text-decoration: none;
		color: #35383E;
	}

	button {
		padding: 0;
		border: 0;
		font-family: inherit;
		cursor: pointer;
		background-color: transparent;
	}

	aside.show {
		opacity: 1;
	}

	aside button {
		border-radius: 5px;
		transition: 0.7s;
	}
	
	aside button:hover {
		background-color: rgba(0, 0, 0, 0.1);
	}
  
	.close-btn {
		align-self: flex-end;
		margin: 20px;
		padding: 1px 10px;
		font-size: 36px;
		color: #35383E;
	}

	aside ul {
		display: inline-block;
		margin: 0 30px 0 0;
	}

	aside li {
		margin: 10px 0;
		padding: 8px 15px 8px 12px;
		list-style-type: none;
		border-radius: 5px;
		transition: 0.7s;
	}
	
	aside li:hover {
		background-color: rgba(0, 0, 0, 0.1);
	}

	.language {
		display: grid; 
		grid-template-columns: 0.3fr 1.7fr; 
		grid-template-rows: 1fr 1fr; 
		grid-template-areas: 
			"language-img language-country"
			". language-spoken"; 
	}

	.language-img {
		grid-area: language-img;
		width: 22px;
	}

	.language-country {
		grid-area: language-country;
		margin: 0;
	}

	.language-spoken {
		grid-area: language-spoken;
		margin: 0;
		padding-top: 5px;
		font-size: 14px;
		color: #626262;
	}

    @media only screen 
	and (max-width: 1200px) {
		aside ul {
			margin: 0 30px 125px 0;
		}
	}

	@media only screen 
	and (max-width: 450px) {
		aside {
			max-width: 80%;
		}
	}
</style>