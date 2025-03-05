<script setup lang="ts">
//ナビゲーションのリンク
type NavItem = {
	link: string;
	linkText: string;
};

const navItems: NavItem[] = [
	{ link: '#works', linkText: '制作実績' },
	{ link: '#profile', linkText: '自己紹介' },
];
</script>

<template>
	<header class="Gh">
		<div class="Gh-inner">
			<h1 class="Gh__logo">
				<a href="/" class="Gh__logo__anchor">深水 佳奈</a>
			</h1>
			<ul class="Gh__nav">
				<li v-for="navItem in navItems" :key="navItem.linkText" class="Gh__nav__item">
						<a :href="navItem.link" class="Gh__nav__anchor">{{ navItem.linkText }}</a>
				</li>
			</ul>
		</div>
	</header>
</template>

<style scoped>
.Gh {
	position: fixed;
	top: 0;
	width: 100%;
	height: 60px;
	z-index: 100;
}

.Gh-inner {
	display: flex;
	align-items: center;
	justify-content: space-between;
	width: 100%;
	height: 100%;
	padding: 0 20px;
	box-sizing: border-box;
}

.Gh__logo {
	font-family: 'Shippori Mincho', serif;
	letter-spacing: 0.1em;
	margin: 0;
}

.Gh__logo__anchor {
	display: block;
	padding: 2px;
	background-color: rgba(255,255,255,1);
}

.Gh__nav {
	display: flex;
	align-items: center;
	list-style: none;
	margin: 0;
	padding: 0;
	font-size: 1.2rem;
}

.Gh__nav__anchor {
	display: block;
	padding: 2px;
	background-color: rgba(255,255,255,1);
}

.Gh__nav__item + .Gh__nav__item {
	margin-left: 1em;
}

@media screen and (min-width: 1024px) {

	.Gh__nav {
		font-size: 1.5rem;
	}

}
</style>