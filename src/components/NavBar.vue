<template>
	<nav id="nav">
		<ul class="nav-list-1">
			<li class="logo"><a href="#"><img src="../assets/tesla-logo.png" alt="Logo of Tesla"></a></li>
		</ul>
		<ul class="nav-list-2" v-if="isNavVisible">
			<li  v-for="item in navList2Items" :key="item"><a href="#">{{ item }}</a></li>
		</ul>
		<ul class="nav-list-3">
			<div class="nav-list-3-items-container" v-if="isNavVisible">
				<li  v-for="item in navList3Items" :key="item"><a href="#">{{ item }}</a></li>
			</div>
			<li><button class="menu-btn" @click="openSidemenu()">Menu</button></li>
		</ul>
	</nav>
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

	function openSidemenu() {
		const sidemenu = document.getElementById("sidemenu");
		const nav = document.getElementById("nav");
		const overlay = document.getElementById("overlay");
		const scrollbarWidth = window.innerWidth - document.body.clientWidth;

		sidemenu.style.width = "330px";
		sidemenu.style.borderLeft = "1px solid #C0C0C0";
		sidemenu.style.opacity = "1";
		document.body.style.overflow = "hidden";

		overlay.style.filter = "blur(4px)";
		nav.style.filter = "blur(4px)";
		overlay.style.transition= "filter 0.3s ease-in-out"
		nav.style.transition= "filter 0.3s ease-in-out"

		document.body.style.marginRight = `${scrollbarWidth}px`;
		sidemenu.classList.add("show");
	}

	function closeSidemenu() {
		const sidemenu = document.getElementById("sidemenu");
		const nav = document.getElementById("nav");
		const overlay = document.getElementById("overlay");

		sidemenu.style.width = "0";
		sidemenu.style.opacity = "0";

		overlay.style.filter = "blur(0px)";
		nav.style.filter = "blur(0px)";
		overlay.style.transition= "filter 0.3s ease-in-out"
		nav.style.transition= "filter 0.3s ease-in-out"

		setTimeout(() => {
			sidemenu.style.borderLeft = "0";
			document.body.style.overflow = "auto";
			document.body.style.marginRight = "0";
			sidemenu.classList.remove("show");
		}, 500);
	}
</script>

<style scoped>
	nav {
		display: flex;
		justify-content: space-between;
		margin: 25px 36px;
		padding: 0;
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
		background-color: transparent;
		cursor: pointer;
	}

	.nav-list-1{
		display: flex;
		margin-left: 10px;
		padding: 0;
	}

	.nav-list-2 {
		display: flex;
		justify-content: center;
		flex-grow: 1;
		margin-left: 50px;
		padding: 0;
	}

	.nav-list-3 {
		display: flex;
		padding: 0;
	}

	.nav-list-3-items-container {
		display: flex;
	}

	nav li {
		padding: 10px 18px;
		list-style-type: none;
		border-radius: 5px;
		transition: 0.7s;
	}
	
	nav li:hover {
		background-color: rgba(0, 0, 0, 0.1);
	}

	.logo:hover {
		background-color: rgba(0, 0, 0, 0);
	}

	nav img {
		width: 125px;
	}

	.menu-btn {
		font-size: 16px;
		font-weight: bold;
		color: #35383E;
	}

	aside {
		display: flex;
		flex-direction: column; 
		position: fixed;
		z-index: 1;
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

	aside.show{
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
	and (max-width: 1350px) {
		nav li {
			padding: 10px 12px;
		}
	}

	@media only screen 
	and (max-width: 1200px) {
		nav li {
			background-color: rgba(0, 0, 0, 0.05);
		}

		.logo {
			background-color: rgba(0, 0, 0, 0);
		}

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
