<script setup lang="ts">
import { computed, ref } from "vue";

/**
 * 同一份內容，一層一層加上去
 * step：0 只有 HTML → 1 加上 CSS → 2 加上 JavaScript（按鈕真的可以按）
 */
const props = withDefaults(defineProps<{ step?: number }>(), { step: 0 });

const s = computed(() => Math.max(0, Math.min(2, props.step)));
const likes = ref(12);
const liked = ref(false);

function like() {
	if (s.value < 2) return;
	liked.value = !liked.value;
	likes.value += liked.value ? 1 : -1;
}
</script>

<template>
	<div class="wl">
		<div class="wl-layers">
			<div class="wl-layer" :class="{ 'is-on': s >= 0 }">
				<span class="wl-tag is-html">HTML</span>
				<span>骨架：有什麼內容</span>
			</div>
			<div class="wl-layer" :class="{ 'is-on': s >= 1 }">
				<span class="wl-tag is-css">CSS</span>
				<span>外觀：長什麼樣子</span>
			</div>
			<div class="wl-layer" :class="{ 'is-on': s >= 2 }">
				<span class="wl-tag is-js">JS</span>
				<span>行為：會怎麼反應</span>
			</div>
		</div>

		<div class="wl-browser">
			<div class="wl-chrome">
				<i />
				<i />
				<i />
				<span>127.0.0.1:5500</span>
			</div>
			<div class="wl-page" :class="{ 'has-css': s >= 1, 'has-js': s >= 2 }">
				<div class="wl-card">
					<div class="wl-avatar">🐉</div>
					<h2>毛哥EM</h2>
					<p>喜歡做網站的龍。</p>
					<ul>
						<li>HTML</li>
						<li>CSS</li>
						<li>JavaScript</li>
					</ul>
					<button :class="{ 'is-liked': liked }" @click="like">♥ 讚 {{ likes }}</button>
				</div>
			</div>
		</div>
	</div>
</template>

<style scoped>
.wl {
	display: grid;
	grid-template-columns: 280px 1fr;
	gap: 40px;
	align-items: center;
}

.wl-layers {
	display: flex;
	flex-direction: column;
	gap: 12px;
}

.wl-layer {
	display: flex;
	align-items: center;
	gap: 12px;
	padding: 12px 14px;
	border-radius: 14px;
	background: var(--surface);
	border: 1px solid var(--hairline);
	opacity: 0.3;
	transition: opacity 0.4s;
}

.wl-layer.is-on {
	opacity: 1;
}

.wl-tag {
	flex: none;
	width: 52px;
	padding: 2px 0;
	border-radius: 6px;
	text-align: center;
	font-family: var(--mono);
	font-size: 12px;
	font-weight: 700;
	color: #fff;
}

.wl-tag.is-html {
	background: #e44d26;
}

.wl-tag.is-css {
	background: #663399;
}

.wl-tag.is-js {
	background: #f0db4f;
	color: #222;
}

.wl-browser {
	border-radius: 14px;
	overflow: hidden;
	border: 1px solid var(--hairline-strong);
	box-shadow: 0 24px 60px -24px rgb(0 0 0 / 0.7);
}

.wl-chrome {
	display: flex;
	align-items: center;
	gap: 6px;
	padding: 8px 12px;
	background: #e9e9ee;
}

.wl-chrome i {
	width: 10px;
	height: 10px;
	border-radius: 50%;
	background: #c9c9cf;
}

.wl-chrome span {
	margin-left: 12px;
	padding: 2px 12px;
	border-radius: 999px;
	background: #fff;
	color: #666;
	font-family: var(--mono);
	font-size: 11px;
}

/* 沒有 CSS：瀏覽器預設樣式 */
.wl-page {
	height: 300px;
	padding: 8px 12px;
	background: #fff;
	color: #000;
	font-family: "Times New Roman", serif;
	font-size: 16px;
	transition: background 0.6s;
}

.wl-card {
	transition: all 0.6s var(--ease);
}

.wl-page h2 {
	margin: 0.3em 0;
	font-size: 1.5em;
	font-weight: 700;
	color: #000;
}

.wl-page p {
	margin: 0.4em 0;
}

.wl-page ul {
	margin: 0.4em 0;
	padding-left: 1.6em;
	list-style: disc;
}

.wl-page li::marker {
	color: #000;
}

.wl-page button {
	padding: 1px 6px;
	border: 1px solid #767676;
	border-radius: 2px;
	background: #efefef;
	color: #000;
	font:
		13px system-ui,
		sans-serif;
	transition: all 0.3s var(--ease);
}

.wl-avatar {
	font-size: 16px;
	transition: all 0.6s var(--ease);
}

/* 加上 CSS */
.wl-page.has-css {
	display: grid;
	place-items: center;
	background: linear-gradient(135deg, #f6d5f7, #fbe9d7);
	font-family: system-ui, sans-serif;
}

.has-css .wl-card {
	width: 260px;
	padding: 20px;
	border-radius: 20px;
	background: #fff;
	box-shadow: 0 12px 30px -12px rgb(80 30 90 / 0.4);
	text-align: center;
}

.has-css .wl-avatar {
	width: 64px;
	height: 64px;
	margin: 0 auto 8px;
	display: grid;
	place-items: center;
	border-radius: 50%;
	background: #f3e8ff;
	font-size: 34px;
}

.has-css h2 {
	margin: 0;
	font-size: 22px;
	color: #6b21a8;
}

.has-css p {
	margin: 4px 0 10px;
	color: #666;
	font-size: 14px;
}

.has-css ul {
	display: flex;
	justify-content: center;
	gap: 6px;
	padding: 0;
	margin: 0 0 14px;
	list-style: none;
}

.has-css li {
	padding: 2px 10px;
	border-radius: 999px;
	background: #f3e8ff;
	color: #6b21a8;
	font-size: 12px;
}

.has-css button {
	padding: 6px 18px;
	border: none;
	border-radius: 999px;
	background: #e9d5ff;
	color: #6b21a8;
	font-size: 14px;
	font-weight: 700;
}

/* 加上 JavaScript：可以按了 */
.has-js button {
	cursor: pointer;
	animation: wl-hint 1.2s ease-in-out 0.6s 2;
}

.has-js button:active {
	transform: scale(0.94);
}

.has-js button.is-liked {
	background: #ec4899;
	color: #fff;
}

@keyframes wl-hint {
	50% {
		transform: scale(1.12);
		box-shadow: 0 0 0 6px rgb(236 72 153 / 0.25);
	}
}
</style>
