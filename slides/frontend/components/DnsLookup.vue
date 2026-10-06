<script setup lang="ts">
import { computed } from "vue";

/**
 * DNS 查電話簿
 * step：0 輸入網址 → 1 問 DNS → 2 DNS 回答 IP → 3 照著 IP 找到伺服器
 */
const props = withDefaults(defineProps<{ step?: number; domain?: string; ip?: string }>(), { step: 0, domain: "www.nycu.edu.tw", ip: "140.113.42.195" });

const s = computed(() => Math.max(0, Math.min(3, props.step)));

// 三個角色的座標（中心點）
const P = {
	client: { x: 110, y: 230 },
	dns: { x: 430, y: 90 },
	server: { x: 750, y: 230 }
};

const ask = computed(() => (s.value >= 1 ? P.dns : P.client));
const answer = computed(() => (s.value >= 2 ? P.client : P.dns));
const packet = computed(() => (s.value >= 3 ? P.server : P.client));
</script>

<template>
	<div class="dns">
		<svg class="dns-lines" viewBox="0 0 860 330" aria-hidden="true">
			<line :x1="P.client.x + 50" :y1="P.client.y - 40" :x2="P.dns.x - 60" :y2="P.dns.y + 10" :class="{ 'is-on': s === 1 || s === 2 }" />
			<line :x1="P.client.x + 70" :y1="P.client.y" :x2="P.server.x - 70" :y2="P.server.y" :class="{ 'is-on': s === 3 }" />
		</svg>

		<div class="dns-node" :class="{ 'is-focus': s !== 1 }" :style="{ left: `${P.client.x}px`, top: `${P.client.y}px` }">
			<div class="dns-url">{{ domain }}</div>
			<img src="../img/imac.svg" alt="" />
			<div class="dns-label">你的電腦</div>
		</div>

		<div class="dns-node dns-book" :class="{ 'is-focus': s === 1 || s === 2 }" :style="{ left: `${P.dns.x}px`, top: `${P.dns.y}px` }">
			<img src="../img/dns-book.svg" alt="" />
			<div class="dns-label">DNS（網路電話簿）</div>
		</div>

		<div class="dns-node" :class="{ 'is-focus': s === 3 }" :style="{ left: `${P.server.x}px`, top: `${P.server.y}px` }">
			<img src="../img/server.svg" alt="" />
			<div class="dns-label mono">{{ ip }}</div>
		</div>

		<div class="dns-bubble" :class="{ 'is-hidden': s < 1 || s >= 2 }" :style="{ transform: `translate(${ask.x}px, ${ask.y - 70}px) translate(-50%, -50%)` }">
			{{ domain.replace(/^www\./, "") }} 在哪？
		</div>
		<div class="dns-bubble is-answer" :class="{ 'is-hidden': s < 2 || s >= 3 }" :style="{ transform: `translate(${answer.x}px, ${answer.y - (s >= 2 ? 150 : 70)}px) translate(-50%, -50%)` }">
			在 {{ ip }}
		</div>
		<div class="dns-packet" :class="{ 'is-hidden': s < 3 }" :style="{ transform: `translate(${packet.x}px, ${packet.y}px) translate(-50%, -50%)` }">
			<img src="../img/box.svg" alt="" />
		</div>
	</div>
</template>

<style scoped>
.dns {
	position: relative;
	width: 860px;
	height: 330px;
	margin: 0 auto;
}

.dns-lines {
	position: absolute;
	inset: 0;
	width: 100%;
	height: 100%;
}

.dns-lines line {
	stroke: var(--hairline-strong);
	stroke-width: 2;
	stroke-dasharray: 6 8;
	transition: stroke 0.4s;
}

.dns-lines line.is-on {
	stroke: var(--purple);
	animation: dns-dash 0.8s linear infinite;
}

@keyframes dns-dash {
	to {
		stroke-dashoffset: -28;
	}
}

.dns-node {
	position: absolute;
	transform: translate(-50%, -50%);
	text-align: center;
	opacity: 0.5;
	transition:
		opacity 0.4s,
		transform 0.4s var(--spring);
}

.dns-node.is-focus {
	opacity: 1;
}

.dns-node img {
	height: 110px;
	width: auto;
	display: block;
	margin: 0 auto;
}

.dns-book img {
	height: 120px;
}

.dns-book.is-focus {
	transform: translate(-50%, -50%) scale(1.08);
}

.dns-label {
	margin-top: 10px;
	font-size: 15px;
	color: var(--dim);
	white-space: nowrap;
}

.dns-url {
	position: absolute;
	left: 50%;
	top: -36px;
	transform: translateX(-50%);
	padding: 4px 12px;
	border-radius: 999px;
	background: var(--ink);
	border: 1px solid var(--hairline-strong);
	font-family: var(--mono);
	font-size: 13px;
	white-space: nowrap;
}

.dns-bubble {
	position: absolute;
	left: 0;
	top: 0;
	z-index: 2;
	padding: 6px 14px;
	border-radius: 14px;
	background: var(--surface-strong);
	border: 1px solid var(--hairline-strong);
	font-size: 15px;
	white-space: nowrap;
	transition:
		transform 1s var(--ease-io),
		opacity 0.35s;
}

.dns-bubble.is-answer {
	border-color: var(--green);
	color: var(--green);
	font-family: var(--mono);
}

.dns-bubble.is-hidden,
.dns-packet.is-hidden {
	opacity: 0;
}

.dns-packet {
	position: absolute;
	left: 0;
	top: 0;
	z-index: 2;
	width: 56px;
	transition:
		transform 1.1s var(--ease-io),
		opacity 0.3s;
}

.dns-packet img {
	width: 100%;
	display: block;
}
</style>
