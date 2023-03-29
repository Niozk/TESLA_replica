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
</template>

<script setup>
    import { ref, onMounted } from 'vue';
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
		sidemenu.style.boxShadow = "0 3px 10px rgb(0 0 0 / 0.2)";
		sidemenu.style.opacity = "1";
		document.body.style.overflow = "hidden";

		overlay.style.filter = "blur(4px)";
		nav.style.filter = "blur(4px)";
		overlay.style.transition= "filter 0.3s ease-in-out";
		nav.style.transition= "filter 0.3s ease-in-out";

		document.body.style.marginRight = `${scrollbarWidth}px`;
		sidemenu.classList.add("show");
	}
</script>

<style scoped>
	nav {
		display: flex;
		justify-content: space-between;
		position: sticky;
		z-index: 2;
		top: 0;
		left: 0;
		right: 0;
		margin: 0 36px 25px 36px;
		padding: 0;
		font-size: 16px;
		font-weight: bold;
		background-color: transparent;
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
	}
</style>