<script setup lang="ts">
import { ref } from "vue";

// 現場示範：真的打一次 API，左邊看 JSON、右邊看結果
const API = "https://dog.ceo/api/breeds/image/random";

const json = ref("");
const image = ref("");
const state = ref<"idle" | "loading" | "error">("idle");

async function load() {
	state.value = "loading";
	try {
		const response = await fetch(API);
		const data = await response.json();
		json.value = JSON.stringify(data, null, 2);
		image.value = data.message;
		state.value = "idle";
	} catch {
		state.value = "error";
	}
}
</script>

<template>
	<div class="df">
		<div class="df-left">
			<button class="df-btn" :disabled="state === 'loading'" @click="load">
				<ph-dog-bold />
				{{ state === "loading" ? "腳踏車出發中…" : "派腳踏車去拿一隻狗" }}
			</button>
			<pre class="df-json">{{ json || "// 按下按鈕，回應的 JSON 會出現在這裡" }}</pre>
			<p v-if="state === 'error'" class="df-error">沒拿到……網路是不是斷了？</p>
		</div>
		<div class="df-photo">
			<img v-if="image" :src="image" alt="隨機狗狗照片" />
			<ph-image class="df-empty" v-else />
		</div>
	</div>
</template>

<style scoped>
.df {
	display: grid;
	grid-template-columns: 1.2fr 1fr;
	gap: 28px;
	align-items: center;
}

.df-left {
	min-width: 0;
}

.df-btn {
	display: inline-flex;
	align-items: center;
	gap: 8px;
	padding: 8px 18px;
	border-radius: 999px;
	background: var(--purple);
	color: var(--ink);
	font-weight: 700;
	transition: transform 0.2s var(--spring);
}

.df-btn:active {
	transform: scale(0.95);
}

.df-btn:disabled {
	opacity: 0.6;
}

.df-json {
	margin-top: 14px;
	min-height: 110px;
	padding: 14px 16px;
	border-radius: 12px;
	background: hsl(231 15% 10%);
	color: var(--green);
	font-family: var(--mono);
	font-size: 12.5px;
	white-space: pre-wrap;
	word-break: break-all;
}

.df-error {
	color: var(--red);
}

.df-photo {
	height: 260px;
	display: grid;
	place-items: center;
	border-radius: 16px;
	overflow: hidden;
	background: var(--surface);
	border: 1px solid var(--hairline);
}

.df-photo img {
	width: 100%;
	height: 100%;
	object-fit: cover;
}

.df-empty {
	font-size: 48px;
	color: var(--comment);
}
</style>
