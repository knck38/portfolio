<script setup lang="ts">
import { ref } from 'vue';

interface WorkItem {
	title: string; //タイトル
	description?: string; //コメント
	thumbnailSrc: string; //サムネイル画像
	popupImgSrc?: string; //詳細画像
	techStack?: string; //使用技術
	role?: string; //担当
	duration?: string; //制作期間
	projectUrl?: string; //制作物のURL
}

const bodyRef = ref<HTMLElement>(document.body);
const activeItem = ref<WorkItem | null>(null);

//WEBアプリ
const appItems = ref<WorkItem[]>([
  {
		title: 'オセロゲーム',
		description: '純粋なJavaScriptとHTML/CSSで作成したオセロゲームです。\nプレイヤーvsプレイヤーで対戦が可能で、石を置ける位置のハイライト機能も実装しました。',
		thumbnailSrc: '/assets/img/appworks_1.png',
		techStack: 'JavaScript（Vanilla JS）、HTML、CSS', 
		projectUrl: 'https://kana.fukami.info/othello/',
  },
  {
		title: 'TODO管理アプリ',
		description: 'Vue + Laravel + MySQL + TailwindCSS を使用して開発したTODO管理アプリです。\nDockerを利用して環境構築を行い、バックエンドとフロントエンドが連携するフルスタックアプリケーションになっています。',
		thumbnailSrc: '/assets/img/appworks_2.png',
		techStack: '・フロントエンド：Vue3、Vite、Inertia.js\n・バックエンド：Laravel12\n・データベース：MySQL\n・環境構築：Docker\n・その他：Tailwind CSS', 
		projectUrl: 'https://todo-app-1-aa8b13eb4274.herokuapp.com/',
  },
]);

//WEBサイト
const webItems = ref<WorkItem[]>([
  { 
		title: '果実農業協同組合連合会',
		thumbnailSrc: '/assets/img/works_1.jpg',  
		popupImgSrc: '/assets/img/works_1_detail.jpg',  
		role: 'マークアップ（下層）、JavaScript、WordPress実装',
		duration: '3ヶ月',
  },
  {
		title: '建設会社',
		thumbnailSrc: '/assets/img/works_2.jpg',
		popupImgSrc: '/assets/img/works_2_detail.jpg',
		role: 'マークアップ、JavaScript、WordPress実装',
		duration: '3ヶ月',
  },
	{
		title: '観光旅館協同組合',
		thumbnailSrc: '/assets/img/works_3.jpg',
		popupImgSrc: '/assets/img/works_3_detail.jpg',
		role: 'マークアップ、JavaScript、WordPress実装',
		duration: '3ヶ月',
  },
	{
		title: '病院',
		thumbnailSrc: '/assets/img/works_4.jpg',
		popupImgSrc: '/assets/img/works_4_detail.jpg',
		role: 'マークアップ（下層）、JavaScript、WordPress実装',
		duration: '3ヶ月',
  },
	{
		title: '通販サイト',
		thumbnailSrc: '/assets/img/works_5.jpg',
		popupImgSrc: '/assets/img/works_5_detail.jpg',
		role: 'マークアップ、JavaScript、Makeshop実装',
		duration: '5ヶ月',
  },
	{
		title: '旅館',
		thumbnailSrc: '/assets/img/works_6.jpg',
		popupImgSrc: '/assets/img/works_6_detail.jpg',
		role: 'マークアップ、JavaScript、WordPress実装',
		duration: '2ヶ月',
  },
	{
		title: '和菓子店',
		thumbnailSrc: '/assets/img/works_7.jpg',
		popupImgSrc: '/assets/img/works_7_detail.jpg',
		role: 'マークアップ（下層）、WordPress実装',
		duration: '2ヶ月',
  },
]);

// ポップアップを開く
const openPopup = (item: WorkItem) => {
  const body = bodyRef.value;

	if (activeItem.value === item) {
		activeItem.value = null;
	} else {
		activeItem.value = item;
		body.classList.add('-show-popup');
	}
};

// ポップアップを閉じる
const closePopup = (): void => {
  const body = bodyRef.value;
  activeItem.value = null;
  body.classList.remove('-show-popup');
};
</script>

<template>
	<section id="works" class="">
		<div class="section-inner">
			<header class="sectionHeader">
				<h2 class="sectionHeader__ttl">制作実績</h2>
			</header>
			<div class="sectionBody">
				<h3 class="">#WEBアプリ</h3>
				<ul class="worksList">
					<li v-for="item in appItems" :key="item.title" 
					:class="{ '-show': activeItem === item }" 
					class="worksList__item appItem">
						<figure class="worksList__img">
							<a @click.prevent="openPopup(item)" class="worksList__img__anchor">
								<img :src="item.thumbnailSrc" :alt="`${item.title}のサムネイル画像`" loading="lazy">
							</a>
						</figure>
						<div class="worksList__popup">
							<div class="worksList__contents">
								<p class="worksList__ttl">{{ item.title }}</p>
								<p class="worksList__comment">{{ item.description }}</p>
								<p v-if="item.projectUrl" class="worksList__link"><a :href="item.projectUrl" target="_blank">{{ item.projectUrl }}</a></p>
								<dl class="discTable">
									<div class="discTable__item">
										<dt class="discTable__lbl">使用技術</dt>
										<dd class="discTable__des">{{ item.techStack }}</dd>
									</div>
								</dl>
							</div>
						</div>
						<p class="worksList__ttl">{{ item.title }}</p>
					</li>
				</ul>
				<h3 class="">#WEBサイト（在職時に制作したもの）</h3>
				<ul class="worksList">
					<li v-for="item in webItems" :key="item.title" 
					:class="{ '-show': activeItem === item }" 
					class="worksList__item">
						<figure class="worksList__img">
							<a @click.prevent="openPopup(item)" class="worksList__img__anchor">
								<img :src="item.thumbnailSrc" :alt="`${item.title}のサムネイル画像`" loading="lazy">
							</a>
						</figure>
						<div class="worksList__popup">
							<div class="worksList__contents">
								<p class="worksList__ttl">{{ item.title }}</p>
								<dl class="discTable">
									<div class="discTable__item">
										<dt class="discTable__lbl">担当</dt>
										<dd class="discTable__des">{{ item.role }}</dd>
									</div>
									<div class="discTable__item">
										<dt class="discTable__lbl">制作期間</dt>
										<dd class="discTable__des">{{ item.duration }}</dd>
									</div>
								</dl>
							</div>
							<figure class="worksList__popup__img">
								<img :src="item.popupImgSrc" :alt="`${item.title}の詳細画像`" loading="lazy">
							</figure>
						</div>
						<p class="worksList__ttl">{{ item.title }}</p>
					</li>
				</ul>
			</div>
		</div>
	</section>
	<div @click="closePopup" class="popup-close"></div>
	<div @click="closePopup" class="popup-overlay"></div>
</template>

<style scoped>
.worksList {
	list-style: none;
	margin: 0;
	padding: 0;
}

.worksList + * {
	margin-top: 3em;
}

.worksList__item {
	width: 100%;
}

.worksList__item + .worksList__item {
	margin-top: 30px;
}

.worksList__img {
	width: 100%;
	position: relative;
	box-sizing: border-box;
	border: 1px solid currentColor;
	margin: 0;
}

.worksList__img:hover {
	border-color: #0000ee;
}

.worksList__img:before {
	display: block;
	content: '';
	padding-top: 62.5%;
}

.worksList__img img {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	vertical-align: bottom;
}

@media screen and (min-width: 768px) {

	.worksList {
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
	}

	.worksList + * {
		margin-top: 1.5em;
	}

	.worksList__item {
		width: calc(50% - 20px);
	}

	.worksList__item + .worksList__item {
		margin-top: 0;
	}

	.worksList__item:nth-of-type(n + 3) {
		margin-top: 30px;
	}

}

@media screen and (min-width: 1024px) {

	.worksList::after {
		content: '';
		width: calc((100% - 80px) / 3);
	}

	.worksList__item {
		width: calc((100% - 80px) / 3);
	}

	.worksList__item:nth-of-type(n + 3) {
		margin-top: 0;
	}

	.worksList__item:nth-of-type(n + 4) {
		margin-top: 40px;
	}
	
}

.worksList__contents {
	max-width: 500px;
	padding: 20px;
	margin: auto;
}

.worksList__contents .worksList__ttl {
	text-align: center;
	margin-bottom: 1.5em;
	padding-bottom: 1em;
	font-size: 1.4rem;
	position: relative;
}

.worksList__contents .worksList__ttl::before {
	content: "";
	display: block;
	width: 60px;
	height: 1px;
	background: #000;
	position: absolute;
	bottom: 0;
	left: 0;
	right: 0;
	margin: auto;
}

.worksList__comment {
	text-align: center;
	margin-bottom: 20px;
	white-space: pre-line;
}

.worksList__link {
	text-align: center;
	margin-bottom: 2em;
}

.worksList__popup {
	position: fixed;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	width: calc(100% - 40px);
	height: calc(100% - 140px);
	max-width: 1000px;
	pointer-events: none;
	opacity: 0;
	overflow: auto;
}

.-show .worksList__popup {
	z-index: 102;
	opacity: 1;
	pointer-events: all;
	transition: opacity 0.4s ease-out;
	background-color: #fff;
}

.appItem .worksList__popup {
	height: auto;
}

.worksList__popup__img {
	margin: 0 auto;
}

.worksList__popup__img img {
	width: 100%;
	vertical-align: bottom;
}

@media screen and (min-width: 768px) {

	.worksList__contents {
		padding: 50px 0px;
	}

	.worksList__contents .worksList__ttl {
		margin-bottom: 50px;
		padding-bottom: 25px;
		font-size: 1.4rem;
	}

	.worksList__link {
		margin-bottom: 60px;
	}

	.worksList__popup {
		width: 80%;
		height: calc(100% - 80px);
	}

}

@media screen and (min-width: 1280px) {
	.worksList__contents .worksList__ttl {
		font-size: 2rem;
	}
}


/* ------ */

.discTable__item + .discTable__item {
	margin-top: 10px;
}

.discTable__des {
	margin: 0;
	white-space: pre-line;
}

@media screen and (min-width: 768px) {

	.discTable__item {
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
	}

	.discTable__lbl {
		width: 100px;
		flex-shrink: 0;
	}

}

@media screen and (min-width: 1280px) {

}

.popup-close {
	position: fixed;
	top: 20px;
	right: 20px;
	width: 40px;
	height: 40px;
	cursor: pointer;
	z-index: 101;
	opacity: 0;
	pointer-events: none;
}

.popup-close:before,
.popup-close:after {
	position: absolute;
	content: '';
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	margin: auto;
	width: 40px;
	height: 3px;
	border-radius: 3px;
	background-color: white;
}

.popup-close:before {
	-webkit-transform: rotate(45deg);
	transform: rotate(45deg);
}
  
.popup-close::after {
	-webkit-transform: rotate(-45deg);
	transform: rotate(-45deg);
}

.-show-popup .popup-close {
	opacity: 1;
	cursor: pointer;
	pointer-events: auto;
}

.popup-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100vh;
	opacity: 0;
	background-color: rgba(0, 0, 0, 0.85);
	-webkit-transition: opacity 0.4s ease-out;
	transition: opacity 0.4s ease-out;
	z-index: 100;
	display: block;
	pointer-events: none;
}

.-show-popup .popup-overlay {
	opacity: 1;
	pointer-events: auto;
}

@media screen and (min-width: 768px) {

	.worksList__popup {
		width: 80%;
		height: calc(100% - 80px);
	}

}

@media screen and (min-width: 1280px) {
	.popup-close {
		top: 40px;
		right: 40px;
	}
}

</style>